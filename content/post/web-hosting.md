+++
title = "Web Hosting"
Categories = []
+++
<div class="zemanta-img">
  <div style="width: 310px" class="wp-caption alignright">
    <a href="http://commons.wikipedia.org/wiki/File:Wordpress-logo.png"><img title="WordPress" src="http://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Wordpress-logo.png/300px-Wordpress-logo.png" alt="WordPress" width="300" height="68" /></a><p class="wp-caption-text">
      Image via Wikipedia
    </p>
  </div>
</div>

For a long time, I wanted to pull the trigger on setting up my own hosting plan for this blog.  The idea being, I could do so much more by hosting my own WordPress instance than I could WordPress.com.  I could choose from a wide variety of themes, plugins, & have complete control over the blog itself to customize it however I saw fit.  So, sometime this past September, I finally pulled the trigger & set up my hosting plan.  Two months later, here I am back on WordPress.com.  I&#8217;ll explain why.

<!--more-->

First off, for those of you who don&#8217;t know me, I&#8217;m an emerging sysadmin by trade.  I love learning how to make a computer do all of the different things that makes our world work today.  I have been a sysadmin for 4 years now, and I&#8217;ve learned a *lot*, yet I&#8217;ve got a *long* way to go.  I remember back when I was just getting my feet wet with Linux.  I remember the frustration, but even more so that awesome feeling you get once it finally works.  This is part of what made the initial idea of hosting my own blog appealing.  I wanted to be able to do more with the skills I had learned.

It had been a while since I&#8217;d really looked into webhosting options, so I googled to see which host was the latest favorite.  Finding this information is not easy, but I recommend the forums at <a href="http://www.webhostingtalk.com" target="_blank">webhostingtalk.com</a>.  During the course of this two month hosting stint, I tried 3 different hosts:  <a href="http://www.bluehost.com" target="_blank">Bluehost</a>, <a href="http://www.ipage.com" target="_blank">iPage</a>, and <a href="http://www.dreamhost.com/" target="_blank">Dreamhost</a>.

<img class="alignnone" title="Bluehost" src="http://www.bluehost.com/media/shared/info/index/_bh/logo.jpg" alt="bluehost" width="209" height="51" />  
After a while of looking around, my first pick was Bluehost.  I got a 3 year plan for $3.95 a month, which included a free domain name.  I thought this was a killer deal, but one day I&#8217;m going to learn to adhere to the old adage &#8220;If it seems too good to be true, it probably is&#8221;. For the most part, Bluehost was fine.  The control panel interface was cPanel driven, so finding what you needed was easy enough.  However, my brain doesn&#8217;t work in cPanel&#8217;s &#8220;Click a button and go&#8221; way anymore.  It&#8217;s more along the lines of &#8220;Type in a string of commands and go&#8221;.  I found myself getting frustrated with the slowness of using a GUI.

<span style="text-decoration:underline;">Things I liked</span>:

1.  Setup was quick & easy.  The longest part was waiting for the DNS registration to complete, which took maybe half a day.
2.  I got shell access to the hosting server after providing a photo ID.
3.  All the usual bells and whistles of a hosting plan were there:  email, mysql, postgresql, cron, dns management, <a href="http://www.bluehost.com/cgi/info/hosting_features" target="_blank">etc</a>.

<span style="text-decoration:underline;">Things I didn&#8217;t</span>:

1.  It was **sloooooooow**.  Everything was slow, even using the shell sometimes I had to wait for my keystrokes to catch up.  The problem was Bluehost&#8217;s DNS servers, which I tracked down via traceroute.  Traceroute showed significant delays, rarely upwards of 300ms & usually averaging 90ms at the longest hop.  Tech support blamed the design of my site (I was using a <a href="http://www.woothemes.com/" target="_blank">WooTheme</a>) & would not admit their DNS servers were a *little* slow.  Searching the forums later showed this is a common problem with Bluehost.
2.  When I chatted with the tech support guy about the slowness, he suggested I close my account if I didn&#8217;t like it.  WTH?
3.  Did I mention it was slow?  Yeah, that&#8217;s pretty much the biggest reason I didn&#8217;t like it.

<img class="alignnone" title="iPage" src="http://webhostingcomparison.org/images/webhosts/ipage.jpg" alt="iPage" width="150" height="40" />  
I kinda set this up on a whim without doing too much research.  At first glance, it looked like a good webhost.  Honestly, what sold me was the *&#8220;NetApp Snapshot Data Backups&#8221;* feature, so I thought they must be cool.  The price was comparable to Bluehost.  However, I was disappointed with the level of control I had once I opened the plan.  I was limited to the control panel, which seemed to be their own custom panel.  It wasn&#8217;t bad, definitely an improvement over the usual cPanel.  The biggest deal breaker for me:  no shell access.  I asked tech support for this feature, and they denied me saying it was a security risk.  Eh?  I blame myself for expecting that while not doing enough research, but I canceled that plan a few days after opening it.  I would recommend it for someone not technical who just wants a webhost.

<img class="alignnone" title="Dreamhost" src="http://images.dreamhost.com/logo.png" alt="dreamhost" width="156" height="33" />  
Of the three I tried, <a href="http://www.dreamhost.com" target="_blank">Dreamhost</a> was by far my favorite.  They have their own custom control panel that seems tailored towards the technical crowd with *plenty* of options in terms of managing all of your services.  They even had an option to run your own Jabber server.  How cool is that??  All the other stuff I wanted, such as shell access, was also there.  Speed was the best of the 3; my site was much more responsive on Dreamhost.  If you take a look at some of their employee profiles, you&#8217;ll see it&#8217;s the kind of company that appeals to the geek crowd.

## **The Result**

So, why am I back on WordPress.com?  Primarily because the host I wanted most, Dreamhost, was slightly too expensive for my taste.  This blog is a hobby, and I can&#8217;t justify putting down $275 up front for a 3 year hosting plan just for a hobby.  Yes, I could get a shorter term plan that&#8217;s cheaper up front, but my feeling is if you&#8217;re going to commit to a website, you do it long term.

This whole process has gotten me to re-evaulate what is most important to me for a blog:

*   I primarily just want to write stuff sometimes, and I want it to look decent while being easy to read.
*   The stuff I write about is usually technical in nature, so things like <a href="http://alexgorbatchev.com/SyntaxHighlighter/" target="_blank">SyntaxHighlighter</a> are nice to have.  I later found this is <a href="http://en.support.wordpress.com/code/posting-source-code/" target="_blank">built into WordPress.com by default</a>.  :)
*   I want to have the posts publicized to social networking sites, primarily Twitter.
*   A reliable host with decent speed.

One of the appeals of using my own hosting plan was the wide array of themes I could chose from.  This kinda backfired.  While I *could* use a lot more themes, I didn&#8217;t find any that I really liked out of the box.  Any one I used would require customization to get it to look how I wanted, and that would take time I didn&#8217;t have.  That&#8217;s why you&#8217;ll notice at the time I posted this, I&#8217;m using the default WordPress theme Twenty Ten with only a modified banner.  I&#8217;m fine with that (at least for now).

Another appeal was having the blog on my own DNS name.  I still want that, but WordPress.com has that option for $14 a year, and I can get the name for $10 a year.  All of a sudden that $100 a year hosting plan is starting to look less and less attractive.

### **VPS**

Ideally, I&#8217;d want a VPS from the likes of <a href="http://mediatemple.net/" target="_blank">MediaTemple</a> or <a href="http://www.linode.com/" target="_blank">Linode</a>.  It would give me all the flexibility and control I wanted, and the reliability of being on an optimal network and hosted in a datacenter.  However, I definitely can&#8217;t justify $30 a month, no matter how much control it gives me.  Maybe one day.

### **The Solution**

For now, I&#8217;m back on WordPress.com and I&#8217;ve canceled all of my shared hosting plans.  I still have my domain name from the Bluehost registration, which I&#8217;ll have for another year per their TOS.  I&#8217;ll be pointing the name to this blog, and I may transfer it to a different registrar at some point.  If I ever get the urge to have &#8220;more control&#8221; over a website to tinker, I&#8217;ll probably do something like set up a VM on my workstation downstairs and use DynDNS with it, and maybe even upgrade my cable plan.  It wouldn&#8217;t be wicked fast, but I&#8217;d bet it would be as fast as those bargain-basement shared hosting plans.  It&#8217;ll at least be enough to satisfy my tinkering urge.  :)
