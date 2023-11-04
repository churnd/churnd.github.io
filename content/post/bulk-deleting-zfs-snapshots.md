+++
title = "Bulk Deleting Zfs Snapshots"
Categories = []
+++
First off, this post will help alleviate some of the guilt I've been having for neglecting my blog.  Second, I just wanted to write it down for my reference.  There's probably a better way to do this but this worked for me.

<!--more-->

I use <a title="NexentaStor" href="http://www.nexenta.com/corp" target="_blank" rel="homepage">NexentaStor</a> at home for my <a title="ZFS" href="http://en.wikipedia.org/wiki/ZFS" target="_blank" rel="wikipedia">ZFS</a>/EXSi All-In-One.  I have a few NexentaStor auto-services set to do ZFS snapshots on each of the filesystems.  I take hourly snapshots kept for a day, daily snapshots that are kept for a week, and weekly snapshots that are kept for a month.  I've been having a problem with some of the snapshots not getting expired.  Since I'm using the community edition, I can't really complain.  I should probably file a bug, but I know the team is busy working on v4.0, which will be awesome.  The admin GUI doesn't have a way that I can see to remove them, so I delved into the command line.

First, you need a list of all the snapshots on the system:

<pre class="lang:default decode:true "># zfs list -t snapshot
NAME USED AVAIL REFER MOUNTPOINT
syspool/rootfs-nmu-030@initial 937M - 1.47G
syspool/rootfs-nmu-030@nmu-024 204M - 1.90G
syspool/rootfs-nmu-030@nmu-025 183M - 1.98G
syspool/rootfs-nmu-030@nmu-026 217M - 2.00G
syspool/rootfs-nmu-030@nmu-027 421M - 2.01G
syspool/rootfs-nmu-030@nmu-028 218M - 2.02G
syspool/rootfs-nmu-030@nmu-029 337M - 2.14G
syspool/rootfs-nmu-030@nmu-030 398M - 2.10G
zpool10@snap-weekly-1-2012-09-08-030002 18K - 33K
zpool10@snap-weekly-1-2012-09-15-030003 0 - 33K
zpool10@snap-weekly-1-2012-09-22-030019 0 - 33K
zpool10@snap-weekly-1-2012-09-29-030010 0 - 33K
zpool10@snap-daily-1-2012-10-02-030003 0 - 33K
zpool10@snap-daily-1-2012-10-03-030008 0 - 33K
zpool10@snap-daily-1-2012-10-04-030006 0 - 33K
zpool10@snap-daily-1-2012-10-05-030025 0 - 33K
zpool10@snap-weekly-1-2012-10-06-030002</pre>

Now copy the names of the snapshots you want to remove & put them in a text file (mine was zfs_cleanup.txt) like this:

<pre class="lang:default decode:true ">zpool10@snap-weekly-1-2012-09-08-030002
zpool10@snap-weekly-1-2012-09-15-030003
zpool10@snap-weekly-1-2012-09-22-030019
zpool10@snap-weekly-1-2012-09-29-030010</pre>

Now you can run a short for loop against the file to remove the snapshots:

<pre class="lang:default decode:true ">#!/bin/bash
file="zfs_cleanup.txt"
while IFS= read -r line
do
# display $line or do somthing with $line
echo "Deleting snapshot $line"
zfs destroy $line
done &lt;"$file"</pre>

If you just have a few snapshots to remove, that's kinda overkill, but I had ~50. Saved me a bit of time. :)
