+++
title = "Migrating From Wordpress to Octopress"
date = "2014-03-30"
slug = "2014/03/30/migrating-from-wordpress-to-octopress"
Categories = []
+++

###Intro

There are a million "Migrating from Wordpress to Octopress" blogs out there.  I didn't want to be yet another one, but I had a few thoughts I wanted to get out there.  Most Octopress blogs I see out there are owned by developers, and I'm a sysadmin.  I had been using Wordpress for a long time, & Blogger before that.  Octopress is... different.

<!-- more -->

###Understanding

The key to successfully migrating from Wordpress to Octopress is to understand how they're different.

Wordpress is a collection of php scripts you dump into a webserver root, install some dependencies, tweak some config files, & setup a database for it to use.  Half of the setup is done through your web browser, & your Wordpress host does all the content generation work.  You create a blog post in your browser most likely, & the content is stored in the database backend.  When a page is requested, Wordpress' php generates it from the database content (usually).  This all happens on the server hosting Wordpress itself.

Octopress is mainly run on your computer.  You set up the computer you're using with some dependencies, download Octopress source code, change it a bit to be specific to your website, run commands to manage it & generate new posts, then upload static html files to your webserver root via rsync (usually).  You're actually generating the site's content on your computer itself, then deploying it to your webserver via some copy method.  All your webserver does is serve static html files.  Cool, huh?  :)

If you were hoping I'd describe how to do it, I defer you here:  [http://octopress.org/docs/](http://octopress.org/docs/ "Octopress Documentation - Octopress").  I've read through those docs many times, as well as other blogs, to gain a better understanding of how Octopress works & how to use it.  Hopefully the two paragraphs above will help you get started quicker.

###Impressions

I migrated to Octopress in October of 2013 (coincidence).  My thoughts of using it so far have been mostly positive.  My VPS only has a measly 1 CPU & 512MB RAM.  It was really struggling to work with the latest Wordpress & php-fpm, constantly running out of RAM & being very sluggish.  Since migrating to Octopress... *Holy Crap*!  My VPS now sits mainly at idle, barely using any resources.  Pages load lightning quick & I have all the plugins I need to generate the kind of content I want.

I was also surprised at how much crap Wordpress injected into my blog posts when I was using it.  Most of the work on my blog from October til now has been fixing the posts, & I'm still not done.  I definitely appreciate Octopress' clean markdown formatting.  I'm writing this blog post in [TextMate](https://github.com/textmate/textmate), which is a great editor for markdown.  I'm still learning it's syntax.

###Advice

Some pointers:

- Realize that Octopress is meant for hackers.  It has a learning curve.  Coming from Wordpress, you won't be comfortable right away.
- You'll have to learn how to use git, rvm, & ruby to manage Octopress.  You don't have to be an expert, but you'll need to learn the basics.
- Don't ignore git.  This will bite you in the ass come upgrade time.  Set up your own repo somewhere (the docs show you how), commit changes, & push them there.  Consider it a backup.
- Be aware of changes you make to your computer that you rely on to generate blog posts.  Changing your environment could mean stuff stops working in your Octopress instance.

###But...

"But... I wanted you to show me how to do it step by step!".

No.

Read... the... docs.  That's the #1 most important step to using Octopress is understanding how it works.
