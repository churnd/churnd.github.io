+++
title = "Os X Server Smb Problems"
Categories = []
+++
The issue is best explained here:  <a href="http://www.stanford.edu/group/macosxsig/blog/2010/01/snow_leopard_samba_and_nt_acl.html" target="_blank">Snow Leopard&#8217;s Samba adds unwanted directives to shares</a>.

The issue I was experiencing specifically was with Windows XP users:

*   User had read/write ACL access to the share.
*   User could create a folder, but not rename it.  User could delete said folder.
*   User could create a file but not rename it.  User could not delete said file.

The fix, unfortunately, involves delving into the OS X command line.  Anyone who thinks that OS X Server can be managed entirely from the GUI will be disappointed.<!--more-->

Before the 10.6.3 update, I was able to get away with using [global] entries in /etc/smb.conf:  
[sourcecode language="bash"]; Site-specific parameters can be added below this comment.  
[global]  
; Hide OS X stuff from Windows Users  
veto files = /.fseventsd/.Trashes/.com.apple.timemachine.donotpresent/.TemporaryItems/TheVolumeSettingsFolder/TheFindByContentFolder/Temporary Items/Network Trash Folder/  
delete veto files = yes  
; Fix ACL&#8217;s for Windows XP Users  
acl check permissions = no  
nt acl support = no[/sourcecode]

Pretty self explanatory. I didn&#8217;t find the ACL fix for Windows XP users&#8230; I got it from the guy who manages the above blog.

So, this worked before 10.6.3 was released. Well, *occasionally* Samba would seem to forget these settings, specifically the veto file directive. In that case, I would bounce the smb service, and all would be good for a while.

With 10.6.3, the problem of Samba forgetting [global] entries got a lot worse. They would work for ~1 day, then quit. I had to do a more destructive bounce of the services smbd & nmbd to get them to work again. That got old quick.

So, following the recommendation of the post above, I added the specific share directives themselves:  
\[sourcecode language="bash"\]\[Backup\]  
acl check permissions = no  
nt acl support = no  
veto files = /.fseventsd/.Trashes/.com.apple.timemachine.donotpresent/.TemporaryItems/TheVolumeSettingsFolder/TheFindByContentFolder/Temporary Items/Network Trash Folder/  
delete veto files = yes  
hide unreadable = yes[/sourcecode]

What a crock.
