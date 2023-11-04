+++
title = "Lacie Rugged Hybrid"
Categories = []
+++
I decided I had to get a <a href="http://www.seagate.com/www/en-us/products/laptops/laptop-hdd" target="_blank">Seagate Momentus XT</a> to compliment my <a href="http://www.ocztechnology.com/products/solid_state_drives/ocz_vertex_series_sata_ii_2_5-ssd" target="_blank">OCZ Vertex SSD</a>.  You know&#8230; for <a href="http://churnd.net/2009/08/14/ssd-upgrade/" target="_blank">educational purposes</a>.  :)

I contemplated putting it <a href="http://eshop.macsales.com/item/Other%20World%20Computing/DDAMBS0GB/" target="_blank">in place of my Superdrive</a>, but the more I thought about it I realized I do still use the Superdrive occasionally.  I glanced over at my <a href="http://www.lacie.com/products/product.htm?pid=11085" target="_blank">LaCie Rugged FW</a> external drive and thought &#8220;That XT would be sweet in that enclosure&#8221; but at first dismissed the idea since there are stickers on the enclosure that clearly state the warranty is voided if they are removed.  I didn&#8217;t want to void the warranty.  Then I thought about it more, & changed my mind.  :)

<!--more-->

I actually did try to carefully remove the stickers with a razor blade but slightly tore one.  If I had been a little more patient, I&#8217;m sure I would have been successful.  However, I made myself feel better by realizing even if the XT fails, I&#8217;m not sending this thing back to LaCie&#8230; I&#8217;m taking the XT out and sending it back to Seagate.  I instantly felt better.

The 500GB Momentus XT was on backorder for 2 months, but finally came in today.  I wasted no time performing the transplant.  The LaCie Rugged enclosure is not difficult to work with.  It&#8217;s held together on the side by metal clamps that snap shut when pressed on.  Once apart, you can see that the drive is secured by a sort of thin plastic wrap that has rubber bumpers which press on the surroundings of the enclosure to hold the drive in place.  I&#8217;ve heard of suspending drives in PC tower cases with rubber bands to help silence them, but that&#8217;s the first time I&#8217;ve seen an external enclosure use rubber bumpers to hold a drive in place.  I guess it does provide additional shock protection in case the drive is bumped or dropped.  Other than that, replacing the drive was as simple as unplugging/re-plugging the SATA connector.

Is it faster?  Yep:

**Pre-Hybrid**  
[sourcecode language="text"]  
Results 32.25  
System Info  
Xbench Version 1.3  
System Version 10.6.4 (10F569)  
Physical RAM 4096 MB  
Model MacBookPro5,1  
Drive Type LaCie Rugged FW/USB  
Disk Test 32.25  
Sequential 66.48  
Uncached Write 77.68 47.69 MB/sec [4K blocks]  
Uncached Write 94.79 53.63 MB/sec [256K blocks]  
Uncached Read 35.68 10.44 MB/sec [4K blocks]  
Uncached Read 114.66 57.63 MB/sec [256K blocks]  
Random 21.29  
Uncached Write 6.82 0.72 MB/sec [4K blocks]  
Uncached Write 73.31 23.47 MB/sec [256K blocks]  
Uncached Read 58.21 0.41 MB/sec [4K blocks]  
Uncached Read 96.51 17.91 MB/sec \[256K blocks\]\[/sourcecode\]

**Post-Hybrid**  
[sourcecode language="text"]  
Results 54.09  
System Info  
Xbench Version 1.3  
System Version 10.6.4 (10F569)  
Physical RAM 4096 MB  
Model MacBookPro5,1  
Drive Type LaCie Rugged FW/USB  
Disk Test 54.09  
Sequential 84.64  
Uncached Write 102.83 63.14 MB/sec [4K blocks]  
Uncached Write 94.12 53.25 MB/sec [256K blocks]  
Uncached Read 50.81 14.87 MB/sec [4K blocks]  
Uncached Read 138.39 69.55 MB/sec [256K blocks]  
Random 39.74  
Uncached Write 12.86 1.36 MB/sec [4K blocks]  
Uncached Write 155.03 49.63 MB/sec [256K blocks]  
Uncached Read 101.48 0.72 MB/sec [4K blocks]  
Uncached Read 152.54 28.31 MB/sec \[256K blocks\]\[/sourcecode\]

I&#8217;m hoping that I&#8217;ll be able to take advantage of that 4GB cache when running virtual machines.  If I configure the machines to split their virtual disks up into 2GB files (and I usually do), loading one 2GB segment entirely in the SSD cache would be no different than running it off of the laptop SSD itself.  However, I am limited by the 80MB/s theoretical maximum speed of the FW800 bus.  eSATA would take care of that problem but it&#8217;s not a native port option on any Apple computer yet, I don&#8217;t have an enclosure as portable as my LaCie that supports one, and I&#8217;m not that greedy&#8230;. yet.  :)  Also, one of the main things I like about the LaCie is that I don&#8217;t have to supply external power.  I very much dislike &#8220;portable&#8221; external enclosures that require a power source.  Kinda defeats the whole portable benefit.

While I&#8217;ve got about 90GB remaining on my 250GB Vertex SSD, I&#8217;ll be moving most of my virtual machines over to my new LaCie Hybrid to see how well they run there.  I don&#8217;t really have any good benchmarks to compare running virtual machines, so my judgement will be entirely &#8220;seat-of-the-pants&#8221;.  If I had thought about it, I would have done more tests such as starting/resuming VM&#8217;s from the old 5400RPM drive & compare to the new XT.  Hindsight is 20/20.  :)
