+++
title = "Zfs on Os X"
Categories = []
+++
About a month ago, an email landed in my inbox from the MacZFS Google group talking about a company called Tens Compliment and how they were bringing <a class="zem_slink" title="ZFS" rel="wikipedia" href="http://en.wikipedia.org/wiki/ZFS">ZFS</a> back to OS X.  I did a double take to make sure it wasn&#8217;t spam.  Much to my delight, it wasn&#8217;t.  Apparently Don Brady, one of <a class="zem_slink" title="Apple" rel="homepage" href="http://www.apple.com">Apple&#8217;s</a> top filesystem engineers & the guy who was working on bringing ZFS to <a class="zem_slink" title="Mac OS X Server" rel="homepage" href="http://www.apple.com/server/macosx/">OS X Server</a>, left Apple recently to found this new startup called Tens Compliment.  I couldn&#8217;t believe it&#8230; it sounded too good to be true, but there it was.  ZFS in all it&#8217;s glory with deduplication, snapshotting, compression, and even full compatibility with OS X ACLs.  I was one of the lucky few who got access to the first public beta so I immediately began trying it out.  I was, and still am, very impressed.  Can&#8217;t wait for the second beta to drop, which will supposedly have a System Preferences control panel for managing your volumes.  Unfortunately, Don replied to my initial email stating his target audience was going to be the Pro-level consumer, not servers.  Can&#8217;t say I blame him since Apple discontinued the <a class="zem_slink" title="Xserve" rel="homepage" href="http://www.apple.com/xserve">Xserve</a>.

<!--more-->

For a while now I&#8217;ve been wanting to get a ZFS presence in my home just because it would be nice having the additional peace of mind that my photos & videos aren&#8217;t silently being corrupted without me knowing.  In the past, this plan would have consisted of a dedicated mini-ZFS server running on a mini-ITX platform tucked away behind my desk.  I remember pricing this setup out once before building off of a cool <a href="http://www.newegg.com/Product/Product.aspx?Item=N82E16811123128" target="_blank">Chenbro</a> box, but it came out to be ~$700 for 4TB RAW disk space.  That&#8217;s a bit much.

Since <a href="http://tenscomplement.com/" target="_blank">Z-410</a> was announced, I&#8217;m back in the game.  Using my Mac Pro, I have two options:

1.  Get an external eSATA enclosure, such as this one from <a href="http://www.newegg.com/Product/Product.aspx?Item=N82E16816111138" target="_blank">SANS DIGITAL</a>, and fill it with 1TB drives. &#8211; $600
2.  Get a <a href="http://eshop.macsales.com/item/Other%20World%20Computing/MM352A52MP8/" target="_blank">mounting bracket from OWC</a>, 2 2.5&#8243; drives & move my boot disks up to the optical bay, freeing up the 4 primary drive bays to use for a RAIDZ1 pool. &#8211; $300-600

Option 1 is most attractive right now because it will still leave plenty of room inside the Mac Pro for other disks & I don&#8217;t have to give up my second optical drive bay.  However, if I went option 2, I&#8217;m considering making those 2 2.5&#8243; drives small-ish SSD&#8217;s for an additional perk, but it&#8217;ll cost more.  I really can&#8217;t decide, but I&#8217;m leaning more towards the SANS DIGITAL enclosure at this point.

For the heck of it, I&#8217;ll post a poll that I&#8217;m sure won&#8217;t get used:

<a id="pd_a_4844681"></a> <div class="PDS_Poll" id="PDI_container4844681" data-settings="{&quot;url&quot;:&quot;http:\/\/static.polldaddy.com\/p\/4844681.js&quot;}" style="display:inline-block;">
</div>

<div id="PD_superContainer">
</div>

<noscript>
  <a href="http://polldaddy.com/poll/4844681">Take Our Poll</a>
</noscript>

Let me know what you think!
