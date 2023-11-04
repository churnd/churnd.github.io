+++
title = "Limiting Your Kids Ipad Usage"
Categories = []
+++

My 3 year old son has been using my wife's <a title="iPad" href="http://www.apple.com/ipad/" target="_blank" rel="homepage">iPad</a> since he was 1.  He's pretty good at it & we think it adds some valuable child development skills.  Of course, we use a heavy duty case, but we haven't really had an instance where he tried to break it.  It's great for things like <a title="Netflix" href="http://www.netflix.com/" target="_blank" rel="homepage">Netflix</a> for Kids & playing Angry Birds, but also educational apps that makes learning how to count & spell more fun.  He's doing pretty well in those areas so we think it's been worth it.  However, we have to be careful not to let him get too addicted to it.  We kinda fell into this rut a little, especially since our second son was born in December & it's easier to let the 3 year old keep himself occupied with the iPad.  We're scaling back, but in the process I looked for ways to make limiting usage a little easier.

<!--more-->

First place I looked were on the <a title="IOS" href="http://www.apple.com/ios/" target="_blank" rel="homepage">iOS</a> restrictions themselves.   Unfortunately there's no time limits there yet.  It would be nice if Apple built something into iOS that locks the device between certain hours or after X amount of hours.  I also looked for a way to limit the volume setting, because my son liked to turn it up full blast all the time.  This doesn't seem to be possible either, at least not universally across apps.  I wound up putting a strip of scotch tape over the speaker, which works pretty well.  The audio is still audible, but at a much more pleasant level.

Second place I looked were 3rd party apps.  I <a href="http://appfinder.lisisoft.com/tag/usage-time-limit.html" target="_blank">found a few</a> like TimeLock & KidTime, but none of them seem to have very solid reviews.  I didn't want to invest the time into getting them working if they weren't going to work well.

Third place I looked was for ideas in limiting device usage on the network.  I have a <a title="PfSense" href="http://www.pfsense.org/" target="_blank" rel="homepage">pfSense</a> box doing all my firewall/routing stuff, so I figured surely there must be a way.  There is, called <a href="http://doc.pfsense.org/index.php/Captive_Portal" target="_blank">Captive Portal</a>, but it's way more complicated than what I'd need.

What I finally wound up doing is going with something I kinda just stumbled upon.  I also have an Apple Airport Extreme at home that serves as my primary wireless access point.  I was browsing through it's settings one day & stumbled upon a feature called Timed Access Control.  It's pretty easy to set up too.  In Airport Utility, select your Airport Extreme, Edit, then click on the Network tab.  You'll see the option at the bottom:

Just check it & click the Timed Access Control button.  A new window will come up where you'll configure the individual devices.  The "default" setting allows all devices, & you can't get rid of it, but you can set wifi usage limits on all devices if you want to.  What you'll want to do is add another device by clicking "+", then giving it a name:

The most important part is identifying the devices MAC address of the wireless device you're trying to limit.  There are several ways to do it, but probably the easiest is to pull it up on the iPad itself:

You can see in the above picture the limits are pretty flexible.  I can set stricter limits during the weekdays, but loosen them up a little on the weekends.  I can already tell I'm going to have fun with this stuff as they get older... setting parental controls & the like.  They'll probably call me evil computer dictator Dad.  I'm OK with that.  This setting has been working as expected, no network traffic on my wife's iPad during certain hours.  It doesn't prevent them from using the iPad completely, but most of what he does involves network related stuff anyway (Netflix), so if that stops working, he usually loses interest.  Win.

That said, this isn't impossible to get around.  Mac addresses can be easily spoofed.  If my 3 year old figures out how to do that on this iPad, I'll let him have it because he's obviously wicked smart & doesn't need me telling him what to do.  :)
