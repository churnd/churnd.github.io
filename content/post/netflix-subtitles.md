+++
title = "Netflix Subtitles"
Categories = []
+++
Earlier this year, Netflix announced the beginning of <a href="http://blog.netflix.com/2010/04/subtitles-now-available-for-some-titles.html" target="_blank">subtitles support for Instant Streaming</a>.  At the time, this only included about 100 episodes of Lost.  Fast forward 5 months and there&#8217;s still no indication of additional support.  While I&#8217;m grateful that something was offered at all, I&#8217;m still wondering what&#8217;s taking so long for additional support.  Other streaming sites such as Hulu have a much more diverse library of tv shows that are subtitled.  If I want to watch a TV show online, I&#8217;ll probably go to Hulu, but most of my online watching consists of movies.  If I want to see a TV show, I&#8217;ll just DVR it at home.

<!--more-->

So, since there are no movies I can see that yet have subtitles in Netflix, watching instantly is kind of useless to me.  So I started looking for ways to use subtitles downloaded freely from other websites.  Initially I was thinking of using VLC somehow since VLC can open an SRT file and overlay it onto the video.  My googling for that idea turned up nil, so I decided to broaden my search & googled &#8220;netflix subtitles&#8221;.  That&#8217;s where I came across <a href="http://josherickson.org/2010/07/28/822/netflix-subtitles" target="_blank">this blog post</a> by Josh Erickson.  That&#8217;s where I learned about the keyboard shortcuts available for the Netflix player, and the ability to embed DFXP subtitle files.  I&#8217;d never heard of DFXP before, but apparently it&#8217;s an XML W3 standard for subtitles.  Cool!  I noticed the script was written in PowerShell, which means Windows only, but a talented Python developer also found the same blog ahead of me and <a href="http://blog.zone38.net/2010/07/28/920/" target="_blank">ported the script to python</a> for us Mac OS or Linux users.  Also worth noting that Josh has developed a GUI for the script that he calls <a href="http://josherickson.org/2010/09/01/875/srt2dfxp-is-now-subvert-also-v0-4-released" target="_blank">Subvert</a> which should be easier for Windows users to use.  Very cool!

Since I&#8217;m primarily a Mac user, I downloaded the python script to try it out.  First I needed to find some (good) SRT files for the movie I wanted to watch.  There are several sites to find subtitles.  I personally haven&#8217;t found a favorite, but if you google &#8220;download subtitles&#8221;, the first page of results will list several good ones.  I usually wind up using <a href="http://www.opensubtitles.org" target="_blank">opensubtitles.org</a> the most.

So now that we&#8217;ve downloaded the python script and the subtitle SRT file we want to use, we need to convert the SRT file to DFXP.  Here&#8217;s how:

First off, you&#8217;re going to have to use the command line. On your Mac, there&#8217;s an application in your Applications, Utilities folder called Terminal.  When you open it, it&#8217;ll look something like this:

<p style="text-align:center;">
  <a href="http://churnd.net/wp-content/uploads/2010/11/terminal.png"><img class="aligncenter size-medium wp-image-482" title="Terminal" src="http://churnd.net/wp-content/uploads/2010/11/terminal.png?w=300" alt="" width="300" height="191" /></a>
</p>

I won&#8217;t go into full detail as to what you&#8217;re seeing here, as it&#8217;s outside the scope of this article.  If you&#8217;re curious, Google &#8220;using bash&#8221;.  So, when you open Terminal.app, you&#8217;re basically looking at a location (directory) on your hard drive.  By default, this is your home directory (Macintosh HD, Users, you&#8230; or /Users/you in Terminal-speak).  If you type the command &#8220;ls&#8221; (without quotes) and hit enter, you&#8217;ll see a printout of your home directory (Desktop, Documents, Photos, Movies, etc).  These are the same as the folders you see in Finder, you&#8217;re just looking at it from the command line interface.

So, assuming you downloaded & unzipped the python script as well as the SRT file for the movie you want to watch, they&#8217;ll most likely be in your Downloads folder.  For simplicities sake, let&#8217;s make a folder in your home directory called &#8220;subtitles&#8221; using Finder.  Go ahead and copy the srt2dfxp.py file (the python script) and the SRT file to this folder.  From the Terminal app, type:

[sourcecode language="bash"]cd subtitles[/sourcecode]

##### *(this is case sensitive, so if you created the folder with a capital S, you&#8217;ll need to type a capital S)*

From there, we need to make sure the srt2dfxp.py file is executable in the shell we&#8217;re in, so we do this by typing

[sourcecode language="bash"]chmod +x srt2dfxp.py[/sourcecode]

and hitting enter. It may be that the file is already executable, but doing this won&#8217;t hurt anything. Now we actually run it:

[sourcecode language="bash"]./srt2dfxp.py[/sourcecode]

or

[sourcecode language="bash"]python srt2dfxp.py[/sourcecode]

which prints out how to use it:

[sourcecode language="bash"]$ srt2dfxp.py  
SubRip to W3 Timed Text (DFXP) Converter v1.3  
Original PowerShell version by Josh Erickson  
Python port by Cody "codeman38" Boisclair

Usage:  
srt2dfxp.py \[-n\] \[-t OFFSET\] INFILE [OUTFILE]  
-n use Netflix-compatible format  
-t add OFFSET seconds to timestamps of original SubRip file  
INFILE input file name  
OUTFILE output file name; will output to STDOUT if omitted[/sourcecode]

So, let&#8217;s say the name of the SRT file is movie.srt, your command to convert it to dfxp would be this:

[sourcecode language="bash"]./srt2dfxp.py -n -t 15 movie.srt movie.dfxp[/sourcecode]

The -n option is for Netflix compatible format (obviously required here). The -t option is to adjust the start time of the dfxp file in case the Netflix stream doesn&#8217;t match up to the original SRT file.

Now we need to load it by switching to the Netflix player and pressing `Ctrl+Shift+Alt+M` simultaneously. Use your mouse to click &#8220;Load Custom DFXP File&#8221;, and then point it to your newly created &#8220;movie.dfxp&#8221; file in the subtitles folder. If it works, you&#8217;ll notice the Subtitles button appears on the player bar:

[<img class="aligncenter size-full wp-image-484" title="Subtitles Menu" src="http://churnd.net/wp-content/uploads/2010/11/menu.png" alt="" width="144" height="223" />][1]

Now, assuming you downloaded a good SRT file and the timing is correct, you&#8217;re good to go!

I experimented the better part of a day with downloading and converting subtitles, then loading them into the Netflix player.  My experience was mixed.  I encountered two main problems:

1.  Some of the DFXP files wouldn&#8217;t load.  I&#8217;m not exactly sure why that is, but I think it is because the SRT file might have been messed up somehow.  It may have also been due to the conversion process.  I don&#8217;t think the Netflix Player will load a file that&#8217;s not w3 compliant.  I did find that if I converted a different SRT file for the same movie, it worked.  I guess it&#8217;s just a matter of finding a reliable source.
2.  The timing of the subtitles is almost always off.  The only way to fix this is to experiment with the -t flag when creating the DFXP file.  It is a very tedious process, because you have to create the file and load it into the Netflix Player each time. According to the guy who wrote the python script:  
    > As for timing, my experience has been that the timing is pretty much the same on all the sites. Typically the issue is that Netflix gets a different print from the studios for streaming than what’s used on the DVD.
    
    So it&#8217;s just a matter of playing around with the times to get it right. One important note is that the -t value can be positive or negative: `-t 15` or `-t -15`. It&#8217;s a little mind bending trying to keep up with which way to adjust the time. On one particular movie, Die Hard 3, I had to adjust the time to -120 and it took me about 30 mins to find the right time!. That was frustrating!</li> </ol> 
    So, once you find the right SRT file and adjust the timing, you&#8217;re good to go. I could understand how one would want to keep these valuable dfxp files around in case they&#8217;re needed later. Someone already came up with that idea, and started posting some to their blog: <a href="http://www.carolinamaria.com/nfsubs/" target="_blank">http://www.carolinamaria.com/nfsubs/</a>.  I&#8217;m going to look around and see if I can find more collections.  I think it&#8217;s a good idea to host DFXP files that have been tested and are known to work, so I&#8217;m going to try to get involved in the collection as well as possibly promote the existing site(s) more.  I have no idea whether or not there are any legal implications with doing so.  I hope not.
    
    I actually thought about trying to write some sort of GUI wrapper to the python script, but I realized it wouldn&#8217;t really help much with making the conversion easier.  What would be **really** cool is if I could figure out some way to have the app read the Netflix Player screen somehow to automatically detect when the movie starts, which would make getting the timing right a lot easier.  Problem is, I have no idea how to do such a thing.  Some kind of audio or visual trigger, even if it were manually done, would probably help a lot.  I guess it would benefit to know how the timing on the SRT file begins, & if there&#8217;s some standard involved.  More to learn&#8230;

 [1]: http://churnd.net/wp-content/uploads/2010/11/menu.png
