+++
title = "Windows Xp X64 on a Mac Pro"
Categories = []
+++
Some of us still prefer XP over 7, and yes, it is possible to use XP x64 on a Mac Pro.  Here&#8217;s how.

First off, I&#8217;m assuming you&#8217;ll want to at least dual boot the Mac Pro between OS X and Windows.  Why not?  The thing has 4 hard drive bays, and if you can afford it at all, filling up those bays is the least of your expenses.

First off, the model of your Mac Pro is important in determining how it works.  I&#8217;ve set up earlier models circa 2006 and they had zero problems assuming you found the right drivers.  More on that in a minute.  The latest model, late 2009/early 2010 will install fine, drivers will install fine, and it will seem to work fine, until you get a blue screen.  Sometimes you&#8217;ll get a blue screen before you can install drivers&#8230; sometimes it&#8217;s much later.  If you have a quick enough eye, you&#8217;ll catch that the blue screen has to do with the disk.sys driver.  The fix is simple:  **Make sure the drive XP is on is connected to the first SATA port on the logic board**.  By default, the DVD/ROM is connected to the first SATA port.  This causes the blue screen.  Switch them, and you&#8217;re set.

The next step is to figure out which drivers to use.  I like using <a href="http://www.cpuid.com/pcwizard.php" target="_blank">PC Wizard</a> from <a href="http://www.cpuid.com" target="_blank">CPUID.com</a>.  The primary thing I&#8217;m looking for is chipset and NIC information.  PC Wizard can usually find these.  I can figure out which graphics card is in it by booting to the OS X side and opening System Profiler in /Applications/Utilities.  Once you have all of this information, it&#8217;s a simple matter of going to Intel&#8217;s and NVIDIA&#8217;s website and downloading the right drivers.  I install the chipset drivers, reboot, install the NIC drivers, then install the graphics drivers, and reboot once again.  At this point, all of the &#8220;major&#8221; components are working in good order.

The only things that do not work that I consider to be unimportant:

1.  Boot Camp Control Panel &#8211; this is useful for choosing your startup disk.  I just hold down option at boot if I want to start up to a different OS.
2.  Keyboard/Mouse drivers &#8211; The wired keyboard works.  The special keys such as volume control, eject, etc don&#8217;t work.  It might be possible to try to install the keyboard drivers from the Boot Camp DVD.  I personally don&#8217;t care about these.  If I need to eject the DVDROM, I&#8217;ll open My Computer, right click on the DVDROM, and click eject.  There are also lots of ways to send the eject command via shortcut on Windows, and creating a shortcut on the desktop.  Google is your friend.  The wireless keyboard and Magic Mouse will not work because Bluetooth does not work.  If I really want a wireless mouse/keyboard, I shell out a few more bucks for something from Logitech that both the Mac and PC side support.
3.  Bluetooth &#8211; does not work, even with trying the Boot Camp DVD drivers.  It&#8217;ll show up as not functioning correctly in Device Manager.  It&#8217;s a Broadcom chipset, so if you want to tinker there, leave a comment if you get it working.

The primary thing I want to use Windows on a Mac Pro for is data processing programs that just work more efficiently in XP than Vista or 7.  The Mac Pro is proving to be great value in that it allows you to consolidate multiple data processing workstations of different operating systems into one, without sacrificing speed.  It&#8217;s a win/win/win situation.  :)
