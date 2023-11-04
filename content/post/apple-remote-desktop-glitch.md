+++
title = "Apple Remote Desktop Glitch"
Categories = []
+++
I manage two Apple XServes at work. We just got the second as a replacement for the first. I just finished setting up the second last night, and the install went pretty smoothly. If you&#8217;re considering the same with the new Intel XServes, I suggest you do your research for known issues and <span style="font-weight:bold;">plan</span> the install. Knowing things like changeip and XServe RAID incompatibilities save lots of headaches.

I still ran into a problem. I use Apple Remote Desktop to manage the servers, but I set it up locally using an LCD, mouse and keyboard. I finished setting it up, and went home. Came in the next day, sat down in front of my Macbook Pro, and tried to login to finish setting permissions to shares. I pulled up the login screen via ARD, typed in my creds, and logged in. I was greeted with this:  
[<img style="display:block;text-align:center;cursor:pointer;margin:0 auto 10px;" src="http://bp0.blogger.com/_z2ziqclKzf0/Rh-4Sxgkx8I/AAAAAAAAAUU/G1iuiXDp7y4/s320/remote.jpg" alt="" border="0" />][1]  
I tried restarting ARD via kickstart and rebooting, but that didn&#8217;t help. So, I tried the admin account instead, and it worked! Obviously the issue was limited to my account. I searched in my ~/Library/Preferences folder for anything related to ARD or VNC, and promptly removed them. This didn&#8217;t help.

I finally got frustrated enough and just removed everything in ~/Library/Preferences (mind you there&#8217;s a tilde (~) in front of that path, so actually /Users/xxxx/Library/Preferences). All this will do is change the look and feel of your account back to it&#8217;s default. Sure enough, it worked! I was then able to log in via ARD.

This is a known issue with ARD, according to [this thread][2] in the Apple support forums. I also tried many of the methods listed in that thread. None of them worked for me. Your mileage may vary.

From what I can tell, the issue has to do with hooking a headless server up to the LCD. The monitor settings get stored in your preferences folder, and can disrupt ARD from working properly. Next time it happens, which I&#8217;m sure it will, I&#8217;ll dig harder for the actual com.apple.xxx.plist file that&#8217;s causing the issues, and if I find it, I&#8217;ll be sure to blog about it again.

 [1]: http://bp0.blogger.com/_z2ziqclKzf0/Rh-4Sxgkx8I/AAAAAAAAAUU/G1iuiXDp7y4/s1600-h/remote.jpg
 [2]: http://discussions.apple.com/thread.jspa?messageID=1566239
