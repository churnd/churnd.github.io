+++
title = "Transmission Clutch a Torrent Server"
Categories = []
+++
I have an openSUSE 11 box at work that I use for testing, development, and file storage.  I resurrected an old RAID array that had a failed RAID controller by pulling out the controller and rewiring it to be just a SCSI chain.  It&#8217;s hooked up to the openSUSE box and configured as a 500GB software RAID5 array.

<div>
  To set up the torrent server, you&#8217;ll need <a href="http://www.transmissionbt.com/">Transmission</a> and <a href="http://clutchbt.com/">Clutch</a>.  Transmission is in the Packman repos, so you can enable that repo via YaST, search for Transmission, and install it.  Or of course, you could download the source and compile it.  If memory serves, I did that once and it compiled easily.
</div>

<div>
  With clutch, it&#8217;s just a bunch of web files made to run on your favorite web server.  I use Apache, so make sure that&#8217;s installed and turned on.  You&#8217;ll also need PHP, JSON for PHP, and the PHP socket extension.  These are all in YaST too.  After they&#8217;re installed, restart the server so they&#8217;ll take affect.  Then unzip the files to the server root, in my case is <span style="font-style:italic;">/srv/www/htdocs/</span>.  I use the web server to test several different things, so I put them in a subdirectory <span style="font-style:italic;">/srv/www/htdocs/clutch</span>, and I can get to it by typing http://server/clutch in my browser.  <a href="http://recurser.com/code/wiki/clutch/Getting_Started">The rest of the instructions are here under the Installation (Linux) section</a>, and the do work fine assuming you follow them step by step.  I know because the first time I tried, I missed a step concerning permissions and had to backtrack to find it.
</div>

<div>
  The important parts in the instructions above are the permissions and file locations.  A key to making this easier for you is knowing which user your web server runs as.  In my case it was <span style="font-style:italic;">wwwrun</span>, and group <span style="font-style:italic;">www</span>.  I edited the necessary files, and did a <span style="font-style:italic;">chown -R wwwrun:www</span> to the top level directory.  Now my web server owns those files and can modify them as needed.
</div>

The last portion of this puzzle is to turn transmission into a service by creating this script in /etc/init.d:  
[sourcecode language="bash"]  
#!/bin/sh  
#  
\# Copyright (C) 2007 JRM  
#  
\# Starts or stops the transmission daemons.  
\# Writes directory permissions and changes owner for  
\# the transmission.socket.&nbsp;

PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin  
NAME="Transmission"  
DESC="torrent daemon"  
SOCK="/opt/transmission/socket"  
DLDIR="/data/Torrents"

case "$1" in  
start)  
echo -n "Starting $DESC: "  
su &#8211; user -c "/usr/bin/transmission-daemon -s /opt/transmission/socket"  
echo "$NAME."  
sleep 2  
chmod -R 777 $SOCK  
chown -R wwwrun:www $SOCK  
sleep 2  
transmission-remote -f $DLDIR  
;;  
stop)  
echo -n "Stopping $DESC: "  
killall transmission-daemon  
echo "$NAME."  
;;  
*)  
N=/etc/init.d/$NAME  
echo "Usage: $N {start|stop}" >&2  
exit 1  
;;  
esac  
exit 0  
[/sourcecode]

I got that script [from this page][1] linked from the clutch directions above, but I modified it a little to fit my needs.  The main thing is who it runs as&#8230; &#8220;user&#8221; on the line [sourcecode language="bash"]su &#8211; user -c &#8230;.[/sourcecode]  You&#8217;ll need to change that to a user on your system that you want the Torrent downloads to belong to. Other things you&#8217;ll need to change are <span style="font-weight:bold;">SOCK</span> and <span style="font-weight:bold;">DLDIR</span>.</div> 

<div>
  Now that you have that set, you can do [sourcecode language="bash"]sudo /sbin/service transmission start|stop[/sourcecode].  From there you should be able to go to the web page and add torrents, and watch them download!  If you want, you can set it to where the service will start on it&#8217;s own with each reboot:  [sourcecode language="bash"]chkconfig transmission on[/sourcecode].
</div>

<div>
  I&#8217;m not really happy with this write-up.  I should have spent more time on elaborating the finer points of permissions and installing the necessary apache/php modules as well as how to start up and configure apache.  I&#8217;ll try to go back and edit that later as time permits.  If you have any questions, please don&#8217;t hesitate to leave a comment.
</div>

 [1]: http://www.mybook-linux.co.nr/transmission.html
