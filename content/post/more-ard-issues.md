+++
title = "More Ard Issues"
Categories = []
+++
I still can&#8217;t track down the [ARD bug][1]. I found an alternative that works: 
1.  Log in via ARD and see the garbled screen
2.  Log in via SSH in the Terminal, and restart ARD using &#8220;sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Conte  
    nts/Resources/kickstart -agent -restart&#8221;
3.  Voila! It&#8217;s fixed!

I&#8217;ll still hunt for the bug until Apple releases a fix.

 [1]: http://hearn.blogspot.com/2007/04/apple-remote-desktop-glitch.html
