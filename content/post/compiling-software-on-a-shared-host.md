+++
title = "Compiling Software on a Shared Host"
Categories = []
+++
During my [shared hosting stint][1], I filled a void of not having root permission to install software by compiling from source to my home directory.  Most shared hosts have a very customized install, and if the host gives you shell access, it doesn't look anything like a regular linux server would (I didn't explore the differences in too much detail).  Two of the three hosts I tried allowed shell access and I was able to compile some basic software on both without a problem.  On the hosts, I successfully compiled <a title="htop" href="http://sourceforge.net/projects/htop/" target="_blank">htop</a>, <a title="rsnapshot" href="http://sourceforge.net/projects/rsnapshot/" target="_blank">rsnapshot</a>, and <a title="rdiff-backup" href="http://www.nongnu.org/rdiff-backup/" target="_blank">rdiff-backup</a>.  I was also using <a title="AutoMySQLBackup" href="http://sourceforge.net/projects/automysqlbackup/" target="_blank">AutoMySQLBackup.sh</a>, but that's just a script (a very good one at that) so it doesn't require any compilation.

<!--more-->

For this article, I'll show you how to compile htop, which is a great alternative to <a title="procps" href="http://procps.sourceforge.net/" target="_blank">top</a> as a systems resource monitor.  htop has very few dependencies to work, so it's a good first project.  I'll use the example account name "demo", but in the code I'll use the shell variable $USER to make the code more copy/paste friendly ($USER in this case = demo). This article assumes you already have shell access to your host and you're logged in and are in your home directory:

{% codeblock %}demo$ pwd
/home/demo/{% endcodeblock %}

Now we need to set up your home directory to compile the software. Most linux systems expect user system-wide compiled software to be in /usr/local, so we'll do a similar strategy here:

{% codeblock %}mkdir ~/local{% endcodeblock %}

Next, you need the source code (get the latest version if it's newer than this):

{% codeblock %}wget http://sourceforge.net/projects/htop/files/htop/0.8.3/htop-0.8.3.tar.gz/download{% endcodeblock %}

Extract it:

{% codeblock %}tar -zxvf htop-0.8.3.tar.gz{% endcodeblock %}

Then change directory to htop:

{% codeblock %}cd htop-0.8.3{% endcodeblock %}

The next step is not very well known, but extremely valuable when compiling from source:

{% codeblock %}./configure --help
--snip--
Installation directories:
--prefix=PREFIX install architecture-independent files in PREFIX
[/usr/local]
--exec-prefix=EPREFIX install architecture-dependent files in EPREFIX
[PREFIX]

By default, `make install' will install all the files in
`/usr/local/bin', `/usr/local/lib' etc. You can specify
an installation prefix other than `/usr/local' using `--prefix',
for instance `--prefix=$HOME'.
--/snip--{% endcodeblock %}

So, we basically need to configure with the prefix flag pointing to "~/local":

{% codeblock %}./configure --prefix=/home/$USER/local{% endcodeblock %}

You should not see any errors once configure completes. If you see any, they will be at the end of the output and will usually indicate there is a missing dependency or something. If that happens, you cannot go further without satisfying the dependency. That's beyond the scope of this article, as it would require compiling more source code to your home directory & setting all sorts of flags and variables to make your environment "sane". So, assuming configure finished without any errors, the rest is easy:

{% codeblock %}make{% endcodeblock %}

(a lot of gibberish passes by -- technical explanation: the code is actually compiling)

{% codeblock %}make install{% endcodeblock %}

(this actually installs the code to /home/$USER/local)

Congratulations! You've successfully compiled htop into your home directory. If you change directory to ~/local, you'll see a few directories were created. Example (your output may have more or less):

{% codeblock %}cd ~/local/
ls -l
total 0
drwxr-xr-x 2 demo demo 68 Nov 21 09:38 bin
drwxr-xr-x 2 demo demo 68 Nov 21 09:38 etc
drwxr-xr-x 2 demo demo 68 Nov 21 09:38 lib
drwxr-xr-x 2 demo demo 68 Nov 21 09:38 man
drwxr-xr-x 2 demo demo 68 Nov 21 09:38 share{% endcodeblock %}

Explanation of these directories:

*   bin --> where the actual binary executable lives
*   etc --> where program (the binary executable) will look for it's configuration files if it has any
*   lib --> any libraries the program depends on will be here
*   man --> the programs man pages are put here&#8230; "man htop"
*   share --> sometimes man pages & other misc docs go here

Now, for the ultimate test: execute the binary to see if it works! You can reference it directly:

{% codeblock %}/home/$USER/local/bin/htop{% endcodeblock %}

If it says something like "File not found", something is missing, so retrace your steps. Assuming everything worked, you should see something similar to this:

{% img /images/uploads/2013/04/htop1.png %}

If you do, congratulations! It's working!

Usually what you do from here is make your environment aware of this new software location by updating your $PATH: (I'm using the editor VIM, but make sure you use whichever editor you're comfortable with. VIM can be frustrating for a first time user)

{% codeblock %}vim ~/.bashrc{% endcodeblock %}

Then add these lines (or modify the existing lines if you already have them):

{% codeblock %}export PATH=~/local/bin:$PATH
export MANPATH=~/local/man:$MANPATH{% endcodeblock %}

Then,

{% codeblock %}. ~/.bashrc{% endcodeblock %}

(this basically tells your shell to read in the new environment)

Now, assuming all that went well, you should be able to just type "htop" and it will start up. You should also be able to do "man htop" to read it's manpage. If all that works, then you are done!

Usually what I like to do is keep the source around in case I ever want to remove the software by "make uninstall", so I usually just create a directory called "software" and move the source code into it:

{% codeblock %}mkdir ~/software
mv ~/htop-0* ~/software/{% endcodeblock %}

That way if I ever want to uninstall the software, I can just do:

{% codeblock %}cd ~/software/htop-0*
make uninstall{% endcodeblock %}

*(Don't do this unless you want to uninstall everything!!)*

So, to sum up, you can take this example and apply it to a lot of different programs assuming you have the source code to compile from. The "./configure -->prefix=" command does all the magic for you. A lot of this is a one time thing (making ~/local and setting up your environment), so if you want to try to compile something else, just do the software specific stuff like downloading, extracting, etc. Happy compiling!

\*\*A Disclaimer\*\* I have no idea if any of this will violate your terms of service with your host. I personally didn't check myself, but I wasn't contacted in the short time I used them. If you are concerned, check with your host.

\*\*A Second Disclaimer\*\* If you see any typos from this, please let me know. I was writing it all from memory \*after\* I canceled my hosting plan.

 [1]: http://churnd.net/2010/11/20/web-hosting/ "Web Hosting"
 [2]: http://churnd.net/wp-content/uploads/2013/04/htop1.png
