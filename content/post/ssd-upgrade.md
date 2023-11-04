+++
title = "Ssd Upgrade"
Categories = []
+++
I finally have a solid state disk in my unibody Macbook Pro.  I can, without a doubt, say this is the single best upgrade I have ever done on any personal computer&#8230; ever.  Forget RAM&#8230; get an SSD.  I used to have to wait ~30 seconds for my Mac to boot completely, login and all.  Granted, I have quite a few things that get started up at login.  Now, it&#8217;s maybe 10 seconds if that.  Apps launch instantaneously.  Decompressing large files is much quicker.  Everything is just faster&#8230; much faster.

Where I work, we are constantly dealing with large medical imaging datasets (such as MRI), which contain tens of thousands of smaller individual files.  So, as you can imagine, disk I/O is very important when cycling through these files for analysis.  At the rate SSD seems to be evolving, it won&#8217;t be long before our data processing workstations will all have one.  So, I needed one to test.  :)

I chose an <a href="http://www.ocztechnology.com/products/flash_drives/ocz_vertex_series_mac_edition_sata_ii_2_5-ssd" target="_blank">OCZ Vertex 250G Mac Edition</a>.  I did extensive research on which drive would be the best candidate to test, and OCZ seems to come out on top quite a bit.  <a href="http://www.anandtech.com/storage/" target="_blank">Anandtech&#8217;s</a> frequent reviews helped a lot.  The new Indilinx controller has been getting rave reviews, so my decision was easy.  If Intel had a 250G option, it would have made my decision much more difficult.

I&#8217;ve been using <a href="http://www.macauthority.com/" target="_blank">MacAuthority</a> to source all of my Apple parts lately, and I&#8217;ve been extremely happy with their service.  I would even go as far to say it&#8217;s the best customer service I&#8217;ve ever received.  Next time you need something, give them a ring.  You won&#8217;t be disappointed.  So, I let them know what I wanted.  They didn&#8217;t carry that specific drive, but it seems all I had to do was let them know I was interested, and they got it for me.  I like that.  :)

<img class="aligncenter size-medium wp-image-243" title="OCZ Vertex 250G Mac Edition" src="http://churnd.net/wp-content/uploads/2009/08/21914605.jpg?w=225" alt="OCZ Vertex 250G Mac Edition" width="225" height="300" />

So, the drive came in, and I wasted no time swapping it with my old 5400RPM disk.  I hooked the old drive up to a SATA to USB controller, booted from it, and proceeded to use <a href="http://www.bombich.com/software/ccc.html" target="_blank">Carbon Copy Cloner</a> to image it onto the SSD.  Unfortunately, halfway through, the SSD disappeared and the clone failed.  &#8221;Don&#8217;t do this to me&#8230; not with my new toy.&#8221;  So, I opened Disk Utility.. no SSD.  I rebooted, tried Disk Utility again&#8230; no SSD.  Tried *ioreg -l -w 0 | grep OCZ*, nothing.  Checked OCZ&#8217;s forums, and found another guy was having a similar problem and they recommended to remove the drive for 30 mins.  So I did, reinstalled it, it showed up!  The forum post recommended doing a firmware upgrade.  Downloaded the ISO, burned it, and rebooted.  It didn&#8217;t recognize the disk.  &#8221;I can&#8217;t believe this&#8221;.  So, I contacted MacAuthority to let them know what happened.  &#8221;OK, we&#8217;re sending you another one right away.&#8221;  Wow, am I a VIP or something?  :)  So, the new one comes in 2 days later.  I immediately check to see if it has the latest firmware, and it does.  I try the clone again, and it works fine this time.  Looking good!

Then I rebooted.  Wow.  I mean **Wow**.  I know I said it above, but wow.  I&#8217;m hardly ever wowed, but this time I was.  **WOW**.

I did before and after benchmarks using <a href="http://www.xbench.com/" target="_blank">XBench</a>.  If you search the Xbench submitted results for &#8220;<a href="http://db.xbench.com/search.xhtml?text=SSD+upgrade" target="_blank">SSD Upgrade</a>&#8220;, you&#8217;ll see mine.  I titled both sumbissions the same, but I misidentified the Macbook Pro the second time so rest assured, they&#8217;re both me.  :)

Pretty definitive results:

*   Pre-SSD &#8211; **37.02**
*   Post-SSD &#8211; **225.84**

So, get one if you haven&#8217;t already (from MacAuthority!).  Sell a kidney if you have to.

I&#8217;m also looking forward to the next firmware upgrade, which is supposed to configure the drive to self-optimize with a garbage collection function and support for TRIM.  A beta version is on the forums as of this posting, but it seems that Mac owners are having problems with their Macs not sleeping properly, so I&#8217;ll wait.  :)
