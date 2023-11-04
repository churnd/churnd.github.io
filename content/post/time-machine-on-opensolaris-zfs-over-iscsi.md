+++
title = "Time MacHine on Opensolaris Zfs Over Iscsi"
Categories = []
+++
I did it.  I finally got Time Machine working over iSCSI on my OpenSolaris RAIDZ1 ZFS pool:

<p style="text-align:center;">
  <a href="http://farm4.static.flickr.com/3552/3404354913_310e2acbab_o.png"><img class="aligncenter" title="OpenSolaris ZFS iSCSI Time Machine" src="http://farm4.static.flickr.com/3552/3404354913_310e2acbab_o.png" alt="Time Machine iSCSI OpenSolaris ZFS" width="350" height="303" /></a>
</p>

For the most part, I followed the instructions here:

<a href="http://opensolaris.org/os/project/qosug/how-tos/zfs_iscsi_integration/" target="_blank">http://opensolaris.org/os/project/qosug/how-tos/zfs_iscsi_integration</a>

Step #6 didn&#8217;t make sense to me (not sure what I was supposed to do), so I skipped it.

It also wasn&#8217;t quite as plug and play as the article suggests.  Here&#8217;s some of the problems I had to overcome:

1.  My SCSI card wasn&#8217;t recognized by OpenSolaris.  <a href="http://groups.google.com/group/comp.unix.solaris/browse_thread/thread/c7d56c4b8c372a8e/7ce3882c18da8d55#7ce3882c18da8d55" target="_blank">This Google Group thread really helped</a>.  Basically, I had to get the SUNWadp driver from a different Solaris distribution (I used <a href="http://opensolaris.org/os/downloads/" target="_blank">SXCE</a>).  I&#8217;m still not clear about how pkgadd works with a directory, so I just copied the uncompressed driver to **/var/spool/pkg** then ran **pfexec pkgadd**.  I also found (via dmesg after rebooting) that the driver is 32-bit only, so I had to remove **$ISADIR** from **/rpool/boot/grub/menu.lst** to boot in 32-bit mode.  I also found out that&#8217;s not really desirable with ZFS as it favors 64-bit but it&#8217;ll have to do until I can find a newer SCSI card.
2.  I had my ZPOOL created, but kept getting errors when I tried to turn on iSCSI.  I then proceeded to try to install the COMSTAR iSCSI target pkg, which didn&#8217;t work.  I found out it was already installed and all I needed to do was enable the service.  Doh!  I&#8217;m still not clear on CLI-fu on OpenSolaris, so I used the Services GUI to do this.  I actually looked for the command to do it via CLI, but it seems to have changed quite a bit from release to release.  I was also getting impatient and wanted results!  :)  The good thing is, the GUI shows you the command, so it&#8217;s a good way to learn.

That&#8217;s it!  Thankfully once I had done that, I was able to connect to the target via the <a href="http://www.studionetworksolutions.com/products/product_detail.php?pi=11" target="_blank">globalSAN iSCSI Initiator for OS X</a>.  I actually expected it not to work, but it worked without a hitch!  I was able to format the ZVOL HFS+ so Time Machine could use it, and my backups began!  This was much faster performance-wise than <a href="http://www.kremalicious.com/2008/06/ubuntu-as-mac-file-server-and-time-machine-volume/" target="_blank">AFP on Linux</a>, and I didn&#8217;t have to trick time machine into using it!

Things I still need to do:

1.  Figure out how to allocate the rest of the ZPOOL and share it via CIFS & hopefully AFP!  How do I tell ZFS to use the rest of the pool?  **zfs create -s -V &#8230;**
2.  Get better with Solaris/OpenSolaris CLI.  Coming from Linux&#8230; it&#8217;s different.
3.  Find a supported SCSI card and use 64-bit.
4.  Figure out how to automatically mount/unmount the volume on my laptop for when I get to work or leave.  The trigger should be whenever I plug in my ethernet cable, but ONLY for that location.  Tricky&#8230;
5.  Figure out iSCSI authentication, such as CHAP.

iSCSI uses a LOT of TCP overhead, so keep that in mind if you&#8217;re doing it yourself.  I have a gigabit switch in my office that all my machines hook into, so that traffic is kept off the main network.  I would not try it over wireless (if that&#8217;s even possible).

The more I learn Sun, the more I&#8217;m realizing it&#8217;s not really for the &#8220;latest and greatest&#8221; technologies, but rather a rock-solid stability.  OpenSolaris seems to be trying to bridge that gap, so I&#8217;m looking forward to seeing where it goes.
