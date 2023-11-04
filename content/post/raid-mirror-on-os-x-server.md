+++
title = "Raid Mirror on Os X Server"
Categories = []
+++
We have two production Tiger servers, and I decided I wanted to get RAID1 set up on the Server HD itself.  Apple tells you this isn&#8217;t possible without reformatting/reinstalling.  AFP548 tells you otherwise:  <a href="http://www.afp548.com/article.php?story=20040827122302975" target="_blank">http://www.afp548.com/article.php?story=20040827122302975</a>

However, I spent several hours trying to get this operational with no success.  If you look in the comments of that article, I&#8217;m not the only one.  I was probably leaving out an important step somewhere, but after a few tries of reformatting, etc, you get a little brain fuzz.  I&#8217;m sure being there at 2am wasn&#8217;t helping either.  :)

I decided against doing this for now.  Instead I opted for a nightly incremental clone using <a href="http://www.bombich.com/software/ccc.html" target="_blank">Carbon Copy Cloner</a> to the second HD.  In hindsight, this is probably going to serve me better.  Let&#8217;s say an update goes awry and renders something unusable.  I still have yesterday&#8217;s clone to boot to!  Hardly anything changes on the server HD itself, since these servers are just file servers, so that works out well.  I can see this not being a good setup for some depending on what kind of server you&#8217;re running and where the important data is actually stored.  In my case, we have 3 Apple RAIDs at ~17TB total (older, but still running), and just bought an <a href="http://www.getactivestorage.com/overview.php" target="_blank">Active XRAID 16TB</a> to compliment that 17TB we already had.  All configured in at least RAID5, with the Active XRAID set up with 2 dual parity RAID6 slices.  Plenty of protection there.  And of course, <a href="http://www.google.com/search?client=safari&rls=en-us&q=raid+is+not+backup&ie=UTF-8&oe=UTF-8" target="_blank">RAID is NOT backup</a>!!

When our next server comes in, I&#8217;ll probably set up a RAID1 mirror with a CCC clone to a single 3rd drive, or maybe use the 3rd drive as a hot spare.  I&#8217;m liking the idea of having an operational 1 day old backup, so the first is more appealing.

On a side note, I&#8217;m interested to see what RAID storage offerings Apple will be offering now that Snow Leopard Server will do ZFS*.

*Apparently, Apple seems to have removed ZFS from it&#8217;s Snow Leopard page.  Say it isn&#8217;t so!!
