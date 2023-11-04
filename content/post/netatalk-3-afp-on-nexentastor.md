+++
title = "Netatalk 3 Afp on Nexentastor"
Categories = []
+++
<a title="NexentaStor" href="http://www.nexenta.com/corp" target="_blank" rel="homepage">NexentaStor</a> is NCP (<a title="Nexenta OS" href="http://www.nexenta.org/" target="_blank" rel="homepage">Nexenta</a> Core Platform) underneath, so you really do have all the power & flexibility of an open unix system.  That's one of the reasons I love the project.  If you want to add on additional functionality, it's not so hard to do so.  Everything I've done to "extend" NexentaStor to my liking has not interfered with the core NMV/NMC functionality.  That said, one of the great things about apt in <a title="Solaris (operating system)" href="http://oracle.com/solaris" target="_blank" rel="homepage">Solaris</a> is apt-clone; something gets messed up, you can revert your system back leveraging the power of ZFS snapshots.  So, when installing a lot of stuff using apt, use apt-clone instead of <a title="Advanced Packaging Tool" href="http://wiki.debian.org/Apt" target="_blank" rel="homepage">apt-get</a>.

One of the things I wanted to use all that disk space I have in my [ZFS/ESXi All-In-One][1] for is Time Machine Backups for the 3 Macs in my house.  I use a combination of Time Machine & CrashPlan for my backups.  Yes, I'm using CrashPlan on NexentaStor as well; that's a future post.

<!--more-->

The recent surge in popularity of the <a title="Mac OS" href="http://www.apple.com/macosx/" target="_blank" rel="homepage">Mac OS</a> has really helped the open source project <a title="Netatalk" href="http://netatalk.sourceforge.net/" target="_blank" rel="homepage">Netatalk</a>.  Netatalk has been around a while, and it's still going strong.  The latest release, v3, looks to have been a big re-write in how Netatalk works.  The biggest change I can see is that configuration is a lot easier & the CNID backends now go into a database rather than "hidden" folders on the shares themselves.  Nice!  Also, the feature we want that's been present since a later version of 2, built-in Time Machine support.

The writeup I pulled from exists on NexentaStor's wiki:  <a href="http://www.nexentastor.org/wiki/site/AFP_with_TimeMachine" target="_blank">http://www.nexentastor.org/wiki/site/AFP_with_TimeMachine</a>.  However, that's for v2, but thankfully v3 is similar.

To start, we need to fall to a "raw" root shell in NexentaStor.  I say "raw" because trying to become root on NexentaStor defaults to NMC (Nexenta Management Console), which is a command-line menu-driven shell designed by Nexenta to manage the main functionality of NexentaStor.  So, to become root from NMC:

{% codeblock Terminal %}nmc@nexentastor:/$ option expert_mode = 1

nmc@nexentastor:/$ !bash
You are about to enter the Unix ("raw") shell and execute low-level Unix command(s). Warning: using low-level Unix commands is not recommended! Execute? Yes

root@nexentastor:/volumes#{% endcodeblock %}

Now we need to install Netatalk's prerequisites.  Thankfully, they are all in the repositories so we don't have to compile any of these from source (that can be a real pain).  Let's install them:

{% codeblock Terminal %}root@nexentastor:~# apt-clone install db4.6-util libdb4.6-dev libssl0.9.8k-dev libldap2-dev{% endcodeblock %}

You may notice netatalk does exist in the repositories as well, but that version is pretty old.  I'm not sure if it supports Time Machine or not.  Anyway, we want v3, so we'll download the source, extract it, and install it:

{% codeblock Terminal %}root@nexentastor:~# wget http://sourceforge.net/projects/netatalk/files/netatalk/3.0.2/netatalk-3.0.2.tar.gz/download

root@nexentastor:~# tar -zxvf netatalk-3.0.2.tar.gz

root@nexentastor:~# cd netatalk-3.0.2{% endcodeblock %}

How we configure the source is the key to getting it working well on NexentaStor, as well as setting things how you like it. "./configure --help" will show you all the available options. Here's what I did:

{% codeblock Terminal %}root@nexentastor:~/netatalk-3.0.2# ./configure --prefix=/usr --sysconfdir=/etc/netatalk --with-init-style=solaris --without-ddp{% endcodeblock %}

I think the most important option in this case is "--with-init-style=solaris", because this will register Netatalk with SMF so we can use it to start/stop it true Solaris style.  The important thing here is you don't want any errors when configure finishes.  The last output of configure should be a summary of your options you configured with (including Netatalk's defaults).  If it errors, it's most likely a missing dependency but we got them all so it shouldn't fail.  The rest is pretty straightforward, typical make install:

{% codeblock Terminal %}root@nexentastor:~/netatalk-3.0.2# make && make install{% endcodeblock %}

In case you aren't familiar, "make" compiles the code how it's specified by "configure" and "make install" puts it all in place & takes care of post-configuration.  The main binary of Netatalk is afpd, so let's check it out:

{% codeblock Terminal %}root@nexentastor:~/netatalk-3.0.2# afpd -v
afpd 3.0.2 - Apple Filing Protocol (AFP) daemon of Netatalk

This program is free software; you can redistribute it and/or modify it under
the terms of the GNU General Public License as published by the Free Software
Foundation; either version 2 of the License, or (at your option) any later
version. Please see the file COPYING for further information and details.

afpd has been compiled with support for these features:

AFP versions: 2.2 3.0 3.1 3.2 3.3
CNID backends: dbd last tdb

afp.conf: /etc/netatalk/afp.conf
extmap.conf: /etc/netatalk/extmap.conf
state directory: /usr/var/netatalk/
afp_signature.conf: /usr/var/netatalk/afp_signature.conf
afp_voluuid.conf: /usr/var/netatalk/afp_voluuid.conf
UAM search path: /usr/lib/netatalk/
Server messages path: /usr/var/netatalk/msg/{% endcodeblock %}

Now we need to define some shares to serve out over AFP.  I will admit the <a href="http://netatalk.sourceforge.net/3.0/htmldocs/configuration.html" target="_blank">documentation</a> on Netatalk's website is a little sparse as to what's available.  "man afp.conf" contains everything you need to know, but the options available can be a little overwhelming to someone not familiar with AFP.  Here's my configuration to give a working example:

{% codeblock Terminal %};
; Netatalk 3.x configuration file
;
 
[Global]
; Global server settings
log file = /var/log/netatalk.log
uam list = uams_dhx.so,uams_dhx2.so
save password = no
aclinherit = passthrough
aclmode = passthrough
 
[Homes]
basedir regex = /home
 
[Software]
path = /tank/Software
 
[Warp]
path = /tank/Warp
time machine = yes{% endcodeblock %}

The value "time machine = yes" enables the Time Machine destination option for that share.  You can see I've created separate ZFS "folders" on the ZFS pool tank.  So my method is to create a ZFS filesystem (folder) if I need a new share, then add it to afp.conf.

Now we turn it on:

{% codeblock Terminal %}root@nexentastor:~/netatalk-3.0.2# svcadm enable netatalk

root@nexentastor:~/netatalk-3.0.2# svcs | grep netatalk
online 11:09:56 svc:/network/netatalk:default{% endcodeblock %}

Netatalk, based on how we've compiled it, will use the local unix user authentication on the system, and it will grant access to shares based on the ACL of the share.  In the NexentaStor web GUI (NMV), make sure your created user has the "unix" option selected.  You will also need to make sure that user or users have access to the ZFS folder by setting the ACL.  You can do this either via the web GUI or command line.

So with Netatalk running, your unix user account created, & permissions set on the ZFS filesystem, you should be able to connect to the Time Machine share then point Time Machine to it to start your backups.

The nice thing about this is we're storing Time Machine backups on ZFS.  When doing Time Machine over the network, it creates SparseBundles on the Time Machine volume.  This allows Time Machine to retain all of the important "extra" HFS+ data, regardless of the filesystem it's on.  So the fact that it's being stored on ZFS doesn't hurt anything as far as losing important OS X specific data that's tied into the filesystem itself.  We also get some additional benefits from using ZFS:

*  No corruption: the SparseBundle format uses "bands", which are 8MB files that contain the actual data.  You could say these bands act like "blocks" do on a hard drive.  ZFS sees these bands just like any other file & protects them accordingly.
*  Compression: Setting compression = on for the Time Machine filesystem we created saves space pretty effectively.
*  Quotas: I can set a ZFS quota on the Time Machine filesystem so it won't use anymore space than I allow.  Netatalk also has an option to limit space used on the share definition, but I prefer the ZFS way.  Allocating more space is as simple as expanding the quota.

I haven't fully tested a restore yet using Netatalk v3, but I have using the older v2 setups in the past.  I should boot to the recovery HD & see if it'll see the Time Machine volume on it's own.  It may need to be mounted manually via command line to be recognized properly.  I have successfully restored via Netatalk v2 in the past, but I had to mount the Time Machine share manually.  Check out "man mount_afp" or Google for this.

I'm only using Time Machine for a "bare metal" type restore situation, in case I need to restore the OS itself.  The reason for this being I don't believe Time Machine is well suited for backing up lots of data.  I use CrashPlan+ to handle my big data backups, which I'm also running on NexentaStor.  That'll be the topic of my next blog post.

 [1]: http://churnd.net/2011/06/27/zfsesxi-all-in-one-part-1/ "ZFS/ESXi All-In-One, Part 1"
