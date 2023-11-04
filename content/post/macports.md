+++
title = "MacPorts"
Categories = []
+++
I love [MacPorts][1].

What a fantastic way to install open source software to run on a Mac. Sometimes I want to be able to run certain Linux/Unix tools on my Macbook Pro, only to find there&#8217;s no Mac alternative available. Or maybe I just prefer to do things the hard way via command line. I&#8217;m weird like that sometimes.

You need Xcode to use MacPorts, so get it and install it if you don&#8217;t already have it: <http://developer.apple.com/tools/xcode/>. It&#8217;s free too!!

Installing it is simple enough as [downloading and installing][2] a PKG. From there you can choose to either control your ports via command line (my personal preference) or a GUI. If you want a GUI, I like [Porticus][3], because it will show you the command as you would type it in Terminal minus sudo. So if Porticus says &#8220;port selfupdate&#8221;, your command in terminal would be &#8220;sudo port selfupdate&#8221; (no quotes).

Setting up Terminal for MacPorts is easy, and outlined on the MacPorts website. I modified my setup a bit from how the website recommended because I test a lot of different software which requires modifying my paths quite a bit. I prefer to keep all these preferences in one place, so I chose my <span style="font-weight:bold;">.bash_profile</span> file in my home directory. I&#8217;ve noticed that if you use <span style="font-weight:bold;">.profile</span> and you have a <span style="font-weight:bold;">.bash_profile</span>, the .bash_profile will take precedence.

If you&#8217;ve never heard of .bash_profile or are wondering why the hell I&#8217;m typing it in with a period in front of the name, you&#8217;re in for a treat. OS X is Unix based, meaning there&#8217;s a LOT that you don&#8217;t see in the file structure using Finder. For example, open up your Terminal Application in /Applications/Utilities/. From there type <span style="font-weight:bold;">ls</span>. You&#8217;re in your User directory, so you&#8217;ll see a list of your user folders such as <span style="font-style:italic;">Documents, Pictures, Desktop, etc.</span> Cool, huh? Now try <span style="font-weight:bold;">ls -l</span>, which basically shows the previous command in a columnar view along with a bunch of other useful information, which I won&#8217;t go into here (that&#8217;s a whole &#8216;nother tutorial). Now try the command <span style="font-weight:bold;">ls -la</span>. Wow! Where did all of that stuff come from?? You&#8217;ll likely see a few files/directories with a period in front of it. What that does is designate a &#8220;hidden&#8221; file or directory. They&#8217;re all there for a reason, so don&#8217;t go trying to delete them unless you know exactly what they do.

Now let&#8217;s set your preferences for MacPorts so you can use it via command line. What you&#8217;ll want to do is create or edit your .bash_profile file, using either vi or nano. Try nano if you&#8217;ve never used a command line editor before, as vi is a little tough to get used to. So once you&#8217;ve opened Terminal, type <span style="font-weight:bold;">nano .bash_profile</span>. A screen will come up:

[<img style="display:block;text-align:center;cursor:hand;margin:0 auto 10px;" src="http://bp2.blogger.com/_z2ziqclKzf0/SA9dMFP1L2I/AAAAAAAAAmQ/2kACG5-Ktzc/s320/nano.png" border="0" />][4]

Yours might not contain any content if it didn&#8217;t previously exist. What you want to do is add the last two lines:

<span style="font-weight:bold;">export PATH=/opt/local/bin:/opt/local/sbin:$PATH<br />export DISPLAY=:0.0</span>

Once you&#8217;ve done that, hit ctrl+x then y to save your changes. Now you&#8217;re back in the regular command line again. Type <span style="font-weight:bold;">source .bash_profile</span> to make the new settings take effect.

Once you&#8217;ve done all this, let&#8217;s test your new settings. Type <span style="font-weight:bold;">which port</span>, and you should get a response that says <span style="font-weight:bold;">/opt/local/bin/port</span>, assuming you installed MacPorts to the default place. If you get that response, you&#8217;re set!

Now you can try a command such as <span style="font-weight:bold;">sudo port selfupdate</span> and type in your password when prompted, which will likely produce the following:

<span style="font-style:italic;">MacPorts base version 1.600 installed</p> <p>
  Downloaded MacPorts base version 1.600
</p>

<p>
  The MacPorts installation is not outdated and so was not updated<br />selfupdate done!</span>
</p>

<p>
  Basically that command checks if there&#8217;s a newer version of MacPorts available. If there was, it would install it by itself. There&#8217;s all kinds of other commands available, such as <span style="font-weight:bold;">sudo port search ___</span> and <span style="font-weight:bold;">sudo port install ___</span>.
</p>

<p>
  You can even try installing something, such as the command line linux downloader <span style="font-weight:bold;">wget</span>. Just type <span style="font-weight:bold;">sudo port search wget</span>, and it will show you the available packages to be installed. Now type <span style="font-weight:bold;">sudo port install wget</span>. What happens next is awesome, because MacPorts fetches each individual source package required to run wget, and compiles it to run on OS X. This is why having Xcode installed is important, because it gives MacPorts what it needs to compile these packages for OS X. Everything is set up in /opt/local/, which pretty much stays out of OS X&#8217;s way. You won&#8217;t have to worry about interfering with critical stuff, because you won&#8217;t.
</p>

<p>
  This is just a basic introduction to MacPorts. Read up on the MacPorts Wiki and get your hands dirty with the Terminal! There&#8217;s all kinds of cool command line (as well as GUI based) applications available.
</p>

 [1]: http://www.macports.org/
 [2]: http://www.macports.org/install.php
 [3]: http://porticus.alittledrop.com/
 [4]: http://bp2.blogger.com/_z2ziqclKzf0/SA9dMFP1L2I/AAAAAAAAAmQ/2kACG5-Ktzc/s1600-h/nano.png
