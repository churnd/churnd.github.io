+++
title = "Exporting Groupwise Mail"
Categories = []
+++
Getting email out of Groupwise isn&#8217;t easy&#8230; at least not by any method I&#8217;ve found. I guess the geniuses at Novell couldn&#8217;t comprehend why anyone would want to use any mail client but theirs.

The method I used to get my mail out was with Outlook. Outlook can connect to the Groupwise mail protocol that it installs by default easily. If you open Outlook after Groupwise has been set up, it&#8217;ll automatically try to connect. Enter the password info and let it set itself up. You can then export your mail to a .PST file to take with you. This works fine&#8230; I&#8217;ve tried it.

However, being a Mac and Mail.app user, my journey didn&#8217;t end there. I read countless of ways to go from Outlook to Mail.app via either Netscape 4.7 or Eudora. Neither of these worked well&#8230; the email wasn&#8217;t formatted properly. I tried a few conversion utilities too&#8230; one even required me import Outlook into Outlook Express, then it would convert the .dbx files to .mbox. It didn&#8217;t work well.

What I wound up doing was this: 
*   From Windows, connect Outlook to Groupwise and let it set itself up.
*   Close Outlook.
*   Download & install [Thunderbird][1], and let it import from Outlook.
*   It will ask for the Groupwise password again&#8230; this means it&#8217;s working, so put it in.

*   Let it import&#8230; this took 30 mins for me.
*   Close Thunderbird and find where it stores your mail in your profile.
*   Usually this will be C:Documents and Settings(user)Application DataThunderbirdProfiles(random).defaultMail
*   Application Data is a hidden folder, so make sure you&#8217;ve enabled the setting to see them in Windows.

*   Copy these to another location. You&#8217;ll notice some large &#8220;files&#8221;<span style="text-decoration:underline;">:</span>[<img style="display:block;text-align:center;cursor:pointer;margin:0 auto 10px;" src="http://bp1.blogger.com/_z2ziqclKzf0/Rie8eIcsaxI/AAAAAAAAAUc/GaWu8nLq1Gs/s320/ishot-2.jpg" alt="" border="0" />][2]
*   These contain your actual mail. Rename these with a .mbox extension.
*   Get these files to your Mac somehow.
*   Open Entourage, and drag and drop these .mbox files onto the Entourage Icon in your Dock. This will prompt you if you want to import them or not. Obviously, say yes.
*   Once you&#8217;ve done them all, you can then tell Mail.app to import from Entourage, and you&#8217;re done.

I actually tried skipping the Entourage part, but I didn&#8217;t like the how Mail.app read the Thunderbird .mbox files. The format was a little off. Bringing them in from Entourage looked much better.![][3]![][3]

 [1]: http://www.mozilla.com/en-US/thunderbird/all.html
 [2]: http://bp1.blogger.com/_z2ziqclKzf0/Rie8eIcsaxI/AAAAAAAAAUc/GaWu8nLq1Gs/s1600-h/ishot-2.jpg
 [3]: ///Users/heatv4/Desktop/ishot-2.jpg
