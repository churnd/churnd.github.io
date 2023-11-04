+++
title = "Photo Libraries"
Categories = []
+++
In this blogger&#8217;s opinion, sharing photos is one of those areas in the computer world that could still use some improvement.  In this particular post, I mean sharing photos in the same household.  My wife and I both keep separate iPhoto libraries on our laptops.  As of this writing, there is no such thing as an iPhoto or Aperture server.  I&#8217;ve made some attempt to try to consolidate them to a common shared storage space on the desktop downstairs using rsync.  For the most part it seems to work, but opening the libraries on a computer in which they were not created or maintained gives mixed results regarding missing settings & plists.  For the most part the settings are there, but it just doesn&#8217;t seem like a solution that would work well in the long run.

<!--more-->

iPhoto and Aperture both support using multiple libraries, but not really a good way managing them together.  Say you have a local iPhoto library that you&#8217;d use to temporarily import photos to post-process on your laptop while you&#8217;re traveling.  At home you have a larger network drive that stores your primary iPhoto library.  The only way to merge the photos from your intermediate library into the primary library is to export them out of iPhoto, switch libraries, then re-import them.  Even then, you&#8217;re losing some of the metadata you might have set in the intermediary library.  Kind of a clunky workflow.

So I took a step back and tried to look at the bigger picture.  Why am I using iPhoto, or any app for that matter, to manage my photos?  Why don&#8217;t I just keep them in a directory structure that I define myself?  So I started thinking of the benefits a photo management app provides (particularly iPhoto):

1.  **Tagging photos with keywords or starring them to make them easier to find.** I hardly ever use this feature and neither does my wife.
2.  **Photos are sorted into events by date.** Sometimes I like this, sometimes I don&#8217;t.  What if an &#8220;event&#8221; to me is a few days?  At present time I have my iPhoto library organized by event, person/people, or place, not so much by date.  It feels like I&#8217;m fighting against what iPhoto wants to do by default by doing this.
3.  **When photos are edited, it copies the photo instead of editing the original**.  Makes it easy to revert back to the original if you ever chose to do so.  I never chose to do so and this takes up more space on my hard drive.
4.  **Sharing options are built in**.  Some of them are useful, some not so much.  I&#8217;ve found that whenever software developers try to keep up with web-based services, it&#8217;s a game they&#8217;re always behind on.  Web services are much easier to update than their software counterparts.  A lot of the options you might get from using a dedicated uploader might not be there in the 3rd party software and when it is, it doesn&#8217;t always work the same.

Not nearly an exhaustive list, by far, but rather some that affect me the most.  So why do I still use iPhoto?  Because reverting back to a directory based structure would be more work up front and in the long run.  It wouldn&#8217;t solve the problem of consolidating photo collections automatically, and would bring other issues into the equation like who has permission to manage what?  What about duplicate photos?  That could easily spiral out of control & actually make it harder to find what you&#8217;re looking for.

It&#8217;s obvious that even if you&#8217;re not using your photo management software&#8217;s full potential, it still alleviates a lot of problems that manual management can bring.  The obvious next step is a centralized server, an iPhoto server.  I&#8217;m not talking about simply storing your iPhoto library on a network volume and using ACL&#8217;s.  I&#8217;m talking about a service built into iPhoto that automatically pushes & pulls changes from a central location to your iPhoto library.  This would also have granular permission control that would give you the ability to assign a person read-only or read-write permissions to an event, for example.  I&#8217;m aware of the iPhoto sharing feature, but that&#8217;s not good enough.  It requires both people to be online and in iPhoto at the same time, which never happens unless they make it happen.

With the current state of personal computing moving to more portable devices, the need to have a centralized server to sync to and pull from is greater than ever before.  I think it&#8217;s only a matter of time before we see it.  Hopefully it won&#8217;t be too long.