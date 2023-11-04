+++
title = "Leopard Server"
Categories = []
+++
With my new (to me) G5 PowerMac, I&#8217;ve been experimenting with Leopard Server all weekend. Things I&#8217;m setting it up to do:

1.  Primarily a Time Machine server.  This works great so far.  Really need an N router w/ gigabit.  I want to stick with DD-WRT, so I&#8217;m looking at the <a href="http://www.amazon.com/Linksys-WRT310N-Wireless-N-Gigabit-Router/dp/B000Z3XXR4" target="_blank">WRT310N</a>, but I want something that&#8217;ll do dual band since I still have legacy (ha!) G devices on my network and don&#8217;t want to suffer speed hits from my N devices.  The <a href="http://www.amazon.com/Linksys-WRT610N-Simultaneous-Dual-N-Wireless/dp/B001AZ01EO/ref=dp_cp_ob_e_title_2" target="_blank">WRT610n</a> is ideal, but DD-WRT <a href="http://www.dd-wrt.com/phpBB2/viewtopic.php?t=33836&postdays=0&postorder=asc&start=750" target="_blank">isn&#8217;t stable</a> on it yet. I don&#8217;t want an Airport Extreme due to lack of local DNS.
2.  OpenDirectory Master.  Mainly just because I want to get better with it.
3.  File Server&#8230; easy enough.  I can definitely appreciate the finer grained controls that ACL&#8217;s provide and being able to use them via Server Admin.  Tiger&#8217;s Workgroup Manager has propagation issues in my experience.  We&#8217;ll see if that&#8217;s the same with Leopard.
4.  Web server & Mysql Server.  For testing stuff.  Apache this time around is so much better.  Reminiscent of a small CMS, with blog & wiki capabilities built in.  I think I&#8217;ll stick with the OS X native versions this time instead of rolling my own.
5.  iCal Server &#8212; if I can get around the infamous <a href="http://discussions.apple.com/thread.jspa?messageID=8685978" target="_blank">Python CPU bug</a>.  Slows the G5 to a crawl!

Bummers:

1.  Only two drive slots and I want at least RAID1, but won&#8217;t do that on the boot drive.  I might add an external FireWire 800 enclosure and RAID that.  For now, I&#8217;m using what I have with the my USB external enclosure and doing backups of the internal Data drive to that.
2.  2GB RAM can get used up pretty quick with all the things I&#8217;m doing.  Probably looking to upgrade to 4GB soon.
3.  Still not convinced Leopard Server is right for that G5.  I&#8217;m wondering what apps won&#8217;t run on it.  Considering partitioning the main HD in half and installing Leopard Client as well.  Kinda defeats the purpose of having a full-time server tho.

Hints:

1.  Make SURE!!! forward and reverse DNS lookups work when installing Leopard Server.  Make your life easier and set up your DHCP/DNS server first!  That&#8217;s why DD-WRT came in handy by creating the static reservation.  Here&#8217;s a hint:  Under the Services tab, set the DHCP server Used Domain to LAN & WAN, then set the LAN domain to **local**.  After that, create a static reservation for the server.  Your end goal, once you have the server installed, is to have `sudo changeip -checkhostname` not throw any complaints. This will also make setting up additional services go smoothly. **Trust me, you WANT to do this FIRST!!** This is what you want to see:  
    > administrator$ sudo changeip -checkhostname
    > 
    > Primary address = 192.168.1.100
    > 
    > Current HostName = Server.local  
    > DNS HostName = Server.local
    > 
    > The names match. There is nothing to change.

What I&#8217;d like to do is actually make the server visible to the world without my ISP knowing about it.  I&#8217;m not sure if I want to do this via proxy or port forwarding or what yet.  I&#8217;ll have to think about it harder.
