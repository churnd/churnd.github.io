+++
title = "Sync Ical With Google Calendar"
Categories = []
+++
I&#8217;ve been trying to find a good way to sync my iCal with Google Calendar.  [Spanning Sync][1] is a good solution, but it&#8217;s not free.  Enter [GCalDaemon][2].  As long as you read the documentation and follow it step by step, it&#8217;s a breeze to configure. <div>
</div>

<div>
  I followed these directions:  <a href="http://gcaldaemon.sourceforge.net/usage13-b.html">http://gcaldaemon.sourceforge.net/usage13-b.html</a>
</div>

<div>
</div>

<div>
  You can use a calendar you already have.  The trick is finding it.  By default, iCal stores it&#8217;s calendar files in:
</div>

<div>
</div>

<div>
  <span class="Apple-style-span" style="font-weight:bold;">/Users/*username*/Library/Application Support/iCal/Sources/</span>
</div>

If you have more than one calendar, you&#8217;ll see folders with a bunch of random characters followed by .calendar.  You can figure out which one is which by opening the Info.plist inside each folder with Property List Editor.  Expand the <span class="Apple-style-span" style="font-weight:bold;">Root</span> key, and the <span class="Apple-style-span" style="font-weight:bold;">Title</span> string will have the name of your calendar. <div>
</div>

<div>
  Once you know which one you want to use, you can point GCalDaemon to it and you&#8217;re set.
</div>

<div>
</div>

<div>
  Also make sure you check out the note about using Lingon to make the script run at startup.  Very useful.  :)
</div>

 [1]: http://spanningsync.com/
 [2]: http://gcaldaemon.sourceforge.net/index.html
