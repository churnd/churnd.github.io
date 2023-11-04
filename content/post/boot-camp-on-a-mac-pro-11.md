+++
title = "Boot Camp on a Mac Pro 11"
Categories = []
+++
Some of <a title="Apple" href="http://www.apple.com" rel="homepage">Apple's</a> earlier hardware has weird <a title="Boot Camp (software)" href="http://www.apple.com/macosx/compatibility/" rel="homepage">Boot Camp</a> support, primarily with 64-bit Windows.  Even though the actual hardware itself is capable of running Windows x64, Apple wouldn't support it.  So, depending on the product line you have, getting the Boot Camp drivers installed could prove tricky.

My workstation at home is a first generation <a title="Mac Pro" href="http://www.apple.com/macpro/" rel="homepage">Mac Pro</a> (MacPro1,1), which is capable of running a 64-bit operating system.  However, Apple doesn't support it; only 32-bit.  That's not good enough for me.  Yes, I could forgo Apple's Bootcamp drivers and hunt down the manufacturer's drivers and that would work fine.  I could even have let Windows install all the drivers for me.  However, I wouldn't have had the little details, like being able to open the optical drive by hitting the eject key.  Those little details drive me nuts.  So, I figured out how to beat Apple at their own game.

<!--more-->

This starts off assuming you've just installed Windows & you're ready to install BootCamp.  As you probably know by now, putting the Snow Leopard DVD in & running the BootCamp installer won't work.  Instead, follow these steps:

1.  Click Start, & type `cmd` & click on the cmd program that comes up in the start menu.
2.  In the command window, type "E:" & hit enter.  Substitute E: for whatever DVD drive your Snow Leopard DVD is in.
3.  Now type `cd Boot CampDriversApple` & hit enter. 
4.  Type `dir` & you should see a list of files, most starting with Apple & 2 starting with BootCamp. 
5.  Now the good stuff; type `msiexec /i BootCamp64.msi` & hit enter.  Boot Camp will now install!

That's half the battle.  Once it installs, you'll reboot & get back into Windows.  Open Apple Software Update & there should be an update to Boot Camp. As of this writing, the latest version is 3.2, so you'll have to update to 3.1 first, then go to 3.2.  However, updating to 3.1 isn't very easy either:
                
1.  With **only** the Boot Camp update selected, click Tools, Download Only.
2.  Once it finishes, click Open Downloaded Updates Folder.  You'll see a file called **BootCamp\_3.1\_64-bit.**
3.  Move this to the upper level of your C: drive to make it easy to work with, or just somewhere easier to get to via command line.
4.  You'll need to extract the contents of this file.  I used 7-zip, which worked great.
5.  With the files extracted, you'll see 3 files (well, I did anyway):  BCUpdateInstaller, BootCampUpdate64, NvidiaGraphics64.
6.  Now you need the command line again, so open a window same as above.
7.  Now the good stuff again; in the command line window, type `msiexec /p C:BootCamp_3.1_64-bitBootCampUpdate64.msp REINSTALL=ALL REINSTALLMODE=omus`
8.  A window will open, click the Repair option. 
9.  The updates will finish installing & ask you to reboot.</ol> 
10.  Once you've rebooted back into Windows, do Apple Software Update again.  Relax, because this time it "just works"!

You'll reboot again & you should be completely up-to-date with all the "official" Apple Boot Camp drivers & software.  You can double check by right clicking on the Boot Camp system tray icon & click About Boot Camp, which should say version 3.2.
                    
Why Apple made it this hard, I have no idea because Windows 7 64-bit runs great on this MacPro1,1.
