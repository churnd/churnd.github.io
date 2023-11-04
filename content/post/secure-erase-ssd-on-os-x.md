+++
title = "Secure Erase Ssd on Os X"
Categories = []
+++
In preparation for Lion, I planned to do a fresh install & wanted to secure erase my <a class="zem_slink" title="OCZ Technology" href="http://www.ocztechnology.com/" rel="homepage">OCZ</a> Vertex 2 SSD to get it working as optimally as possible.  Nothing like a shiny new OS, ridden of all the cruft that builds up over the years.  The problem?  No easy way to secure erase an SSD in a <a class="zem_slink" title="Macintosh" href="http://www.apple.com/mac/" rel="homepage">Mac</a> that doesn&#8217;t involve using some Windows tool on one of a few compatible SATA controllers that your Mac probably doesn&#8217;t have.  It&#8217;s possible, but not very easy.  It requires using hdparm & a compatible Linux LiveCD.

<!--more-->

You can use \*ANY\* linux livecd you want, as long as it includes the appropriate graphics card drivers for your model Mac.  I tried several & wound up using <a class="zem_slink" title="PCLinuxOS" href="http://www.pclinuxos.com/" rel="homepage">PCLinuxOS</a>.  The reason you need the graphics drivers is because you need to be able to suspend the Mac to RAM & wake it back up reliably.  In my experience, this is only easily done if the graphics drivers are installed & I&#8217;m not aware of a way to &#8220;install&#8221; them in a LiveCD while it&#8217;s running.  If you can&#8217;t get the graphics driver loaded, none of this will work.

I&#8217;m not going to repeat all of the instructions for doing the secure erase, as they&#8217;re very well documented in the <a href="https://ata.wiki.kernel.org/index.php/ATA_Secure_Erase" target="_blank">SSD ATA Secure Erase Wiki</a>.  I will go over the process it took me to suspend & wake up my 2008 Macbook Pro, effectively &#8220;thawing&#8221; out the SSD from it&#8217;s frozen state that hdparm reports it to be in.

This assumes you&#8217;ve burnt your LiveCD already & it is in your Mac&#8217;s optical drive.  Restart your Mac & hold down option to bring up the available boot items screen.  Wait a minute for the optical drive to spin up & you&#8217;ll see a disc come up humorously labeled &#8220;Windows&#8221;.  Hit enter & PCLinuxOS will start booting up.  This can take a while.  Once you&#8217;re up & running, you need to suspend to RAM (click Start, Suspend).  The suspend works great, thanks to the right graphics driver being loaded.  There&#8217;s a slight glitch resuming, though.  When you resume, the screensaver is going to ask you for a password & I don&#8217;t know what it is.  There are two ways to handle this:

1.  Remember to set the password before suspending either using the GUI tool for managing user accounts or the command line tool &#8220;passwd&#8221;.  I never tried it because I kept forgetting to do it before suspending.
2.  Hit ctrl+alt+f5 to fall back to a root shell & kill the screensaver process (find it by ps -ax), then hit ctrl+alt+f7 to get back to the GUI.

Once you&#8217;ve verified the drive is no longer frozen as the tutorial above states, you can then proceed to secure erase the drive.  I successfully did this on my 2009 model unibody Macbook Pro with NVIDIA GPU&#8217;s.  I suspect those with ATI \*might\* have more trouble due to the bad ATI driver support on Linux.

I&#8217;ve also found <a href="http://www.ocztechnologyforum.com/forum/showthread.php?81321-Secure-Erase-With-bootable-CD-USB-Linux..-Point-and-Click-Method" target="_blank">this tutorial</a> after I used this method, which looks like it&#8217;s a lot easier, but I have not tried it.
