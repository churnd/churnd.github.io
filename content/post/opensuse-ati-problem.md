+++
title = "Opensuse Ati Problem"
+++
\*\*UPDATED\*\*

Today I realized that changing the below mode from 0660 to 0666 is not the right way to go.  There is an actual group in OpenSUSE called &#8220;video&#8221; that each user needs to be a member of.  The &#8220;mode&#8221; is actually a permission that gives users of the group &#8220;video&#8221; access to the special DRI 3D stuff that the video card does.

Well, by default, all users in OpenSUSE are a member of the video group.  I happened to be using <a href="http://www.cyberciti.biz/faq/howto-move-migrate-user-accounts-old-to-new-server/" target="_blank">this method of migrating users</a> to upgrade the workstation so I wouldn&#8217;t lose any passwords.  Somehow, the users lost their video group membership, most likely due to the differences between OpenSUSE 10.3 and 11.  That caused the error below.

\*\*/UPDATED\*\*

Thought I&#8217;d post this so maybe it&#8217;ll help someone else later.

After upgrading one of our workstations to OpenSUSE 11, I had a problem getting the ATI Drivers to load properly.  I tried both the drivers in ATI&#8217;s YaST repository as well as the one available for download from their website.  The problem persisted with either method.  I have an ATI FireGL V5200 card.  Here&#8217;s the error I saw:

> fglrxinfo  
> libGL error: open DRM failed (Operation not permitted)  
> libGL error: reverting to (slow) indirect rendering

After about half a day of researching the issue, I found the fix.  At the very end of your /etc/X11/xorg.conf, you should see this section:

> Section &#8220;DRI&#8221;  
> Group      &#8220;video&#8221;  
> Mode       0660  
> EndSection

Change the Mode to **0666**, then restart X by hitting ctrl+alt+backspace twice (some only once).  Problem solved!  I have no idea if this is a security risk or not, so leave a comment if it is.
