+++
title = "Uac Workaround"
Categories = []
+++
UAC in Vista sucks, that&#8217;s no secret. You can disable it, but doing so can cause potential problems with software not working like it should. Luckily, you can leave it on and keep your sanity at the same time.

*   First, re-enable UAC if you&#8217;ve already disabled it
*   Open Control Panel and search for Administration Tools
*   Click Local Security Policy, then Local Policies
*   Click Security Options
*   Click &#8220;User Account Control: Behavior of the elevation prompt for administrators in Admin Approval Mode&#8221;
*   Change the status to &#8220;Elevate without prompting&#8221;
*   Done

Now UAC works like it should, and doesn&#8217;t bug the crap out of you every 5 mins. <img src='http://churnd.net/wp-includes/images/smilies/icon_smile.gif' alt=':)' class='wp-smiley' /> This only affects administrator accounts, so regular user accounts still get the prompts. Best of both worlds if you ask me!

You can also try <a href="http://www.tweak-uac.com/download/" target="_blank">TweakUAC </a>which I think does the same thing, but I haven&#8217;t tried it.

Yes, I&#8217;m back to Vista again. I&#8217;m weak, I know. Honestly, I think my mind was playing tricks on me in terms of performance, because I didn&#8217;t notice that much difference using XP for 2 weeks. The only thing that really stood out was file copy performance. It still gets on my nerves, but I&#8217;m sure there&#8217;ll be a fix soon, with SP1.
