+++
title = "Switching Time MacHine Destinations"
Categories = []
+++
I back up my Macbook Pro using Time Machine to OS X server at both work and home.  Two different backups.  The more the better, right?  The only thing I didn&#8217;t like was having to switch the TM destination manually by going into System Preferences, Time Machine, etc.  Lots of clicks.  &#8221;I need automagic&#8221;, I thought.  After a lot of Googling, I came up with a way that works.  Here&#8217;s how.<!--more-->

First off, you need to figure out how Time Machine remembers it&#8217;s backup destination.  You can do this by running this command in the Terminal:

[sourcecode language="bash"]defaults read /Library/Preferences/com.apple.TimeMachine BackupAlias[/sourcecode]

. That&#8217;ll output some really long string of characters. I have no idea what they mean, but that is how Time Machine remembers which disk/volume it is using. It&#8217;ll look something like this:

[sourcecode language="bash"]00000000 03aa0002 00010642 61636b75 70000000 00000000 00000000 00000000 00000000 0000c79e f1f5482b 00010000 00010642 61636b75 70000000 00000000 00000000 &#8230;&#8230;.. 00000668 65617476 34000018 00206166 703a2f2f 68656174 76344044 61727769 6e2e6c6f 63616c2f 4261636b 7570ffff 0000[/sourcecode]

. I cut my output short because it&#8217;s pretty long, but you&#8217;ll need your entire output from one < to the last >. You&#8217;ll need both of these strings of numbers for each Time Machine destination. The only way I know how to get them is to set it in Time Machine preferences first, then do the defaults read to get the value.

&nbsp;

Once you have both, we&#8217;ll need to put each in it&#8217;s own respective shell script, like so:

[sourcecode language="bash"]#!/bin/bash  
defaults write /Library/Preferences/com.apple.TimeMachine BackupAlias &#8217;00000000 03aa0002 00010642 61636b75 70000000 00000000 00000000 00000000 00000000 0000c79e f1f5482b 00010000 00010642 61636b75 70000000 00000000 00000000 &#8230;&#8230;.. 00000668 65617476 34000018 00206166 703a2f2f 68656174 76344044 61727769 6e2e6c6f 63616c2f 4261636b 7570ffff 0000&#8242;[/sourcecode]

. So when you&#8217;re done you&#8217;ll have two different scripts. Make sure they&#8217;re executable by doing

[sourcecode language="bash"]chmod +x script.sh[/sourcecode]

. After that, you can actually run them to verify it does change your Time Machine destination just by doing

[sourcecode language="bash"]./script.sh[/sourcecode]

, then going into Time Machine preferences and seeing what destination has been set. If it works, put both scripts somewhere out of the way and leave them there. I have a folder in my home directory

[sourcecode language="bash"]~/Library/Scripts/[/sourcecode]

where I keep various Applescripts, so I put them there. They do not actually have to be in your user or system path ($PATH) based on how we&#8217;re setting it up, but it won&#8217;t hurt either way.

&nbsp;

Now we&#8217;ve got the backend of switching Time Machine destinations set up, we need a way to trigger it. I wanted to do this based on my IP address, because my work IP address range is different from at home. To do this, I&#8217;m using <a href="http://www.symonds.id.au/marcopolo/" target="_blank">MarcoPolo</a>. It took me a while to figure out how MarcoPolo works, but it&#8217;s basically like this (assuming I understand it correctly):

*   A &#8220;context&#8221; in MarcoPolo is basically a set of rules.
*   Whatever &#8220;context&#8221; is active, only the rules that belong to it will be in effect.

Since I&#8217;m only using MarcoPolo for one purpose at this time, I only have one context, and two rules. This wasn&#8217;t evident to me at first, because I couldn&#8217;t figure out how to tell which rule would trigger which action. The best I can tell is that they&#8217;re in order&#8230; the first rule will trigger the first action, and so on. Not 100% clear on that yet.

So my first rule is for my home network, which only has one subnet, so it was easy to configure:

[<img class="aligncenter size-medium wp-image-305" title="Home IP Rule" src="http://churnd.net/wp-content/uploads/2010/04/screen-shot-2010-04-08-at-7-35-21-pm.png?w=300" alt="" width="300" height="227" />][1]

The second rule was for work, and based on my location between various buildings, my IP address could change quite a bit. I thought of making the rule specific to the subnet I&#8217;m on when I&#8217;m in my office, but I decided to go with the entire IP range:

[<img class="aligncenter size-medium wp-image-307" title="Work IP Rule" src="http://churnd.net/wp-content/uploads/2010/04/screen-shot-2010-04-08-at-7-35-40-pm.png?w=300" alt="" width="300" height="227" />][2]

After that, I set up the actions to correspond with the order of the rules:

[<img class="aligncenter size-medium wp-image-309" title="IP Actions" src="http://churnd.net/wp-content/uploads/2010/04/screen-shot-2010-04-08-at-7-42-41-pm1.png?w=300" alt="" width="300" height="226" />][3]

I set the delay on the actions just to give the OS time to get settled with other network based events that might be going on.  I&#8217;m sure you could do without it, I&#8217;m just weird that way.

So, this morning when I got to work, it didn&#8217;t work out for me because I was misunderstanding the purpose of contexts.  I thought you had to have a different context for each rule.  :(  But I did verify that the tm_work.sh script did switch my Time Machine backup destination and I kicked off the backup manually, which worked fine.

When I got home after work, I got back online to see if MarcoPolo would do it&#8217;s magic.  Sure enough, it did.  I&#8217;ll watch it over the next few days to make sure it switches and backs up reliably, but this is looking to be a great way to have more than one Time Machine destination.

 [1]: http://churnd.net/wp-content/uploads/2010/04/screen-shot-2010-04-08-at-7-35-21-pm.png
 [2]: http://churnd.net/wp-content/uploads/2010/04/screen-shot-2010-04-08-at-7-35-40-pm.png
 [3]: http://churnd.net/wp-content/uploads/2010/04/screen-shot-2010-04-08-at-7-42-41-pm1.png
