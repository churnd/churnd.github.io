+++
title = "Dd Wrt Dns Forwarding"
Categories = []
+++
One of the (many) nice things about DD-WRT is that it has a built-in,  lightweight DNS server that you can use as a DNS forwarder.  Also, one of the primary things that controls how "fast" a network feels for you is the amount of time it takes to resolve a domain name.  Resolving a domain name means that if you type in "www.google.com" in your browser, the browser sends a request to whatever DNS server you're using, asking "Hey, what computer IP address does this domain name belong to?", and finally routing the request to the computer or server.  The quicker you can get this request resolved, the faster your browsing experience is going to feel.

<!--more-->

If you have not changed your DNS settings at all, you're using whatever DNS servers your ISP provides.  However, ISP's are in the business to make money first, so they're always looking for additional sources of income.  Lately, one of these has been to redirect "mistyped" dns requests to a search page filled with advertisements such as "www33.not-found-entry.org".  If you use a Mac like I do, one of the well known features is you can just type in a domain name without the "www" or "com" in Safari & it fills out the rest for you.  However, as soon as my ISP (Insight Cable) <a href="http://www.dslreports.com/forum/r19320257-www33.not-found-entry.org" target="_blank">started doing this DNS redirection</a>, Safari autocomplete stopped working & I kept getting redirected to the "www33." search page.  Not cool at all.

Luckily, you're not locked into using your ISP's DNS servers.  There are publicly available DNS servers that don't do anything to hijack your browser & in most cases are faster.  Some of my favorites:

1.  **Level3** 
    *   4.2.2.1
    *   4.2.2.2
    *   4.2.2.3
    *   4.2.2.4
    *   4.2.2.5
    *   4.2.2.6
2.  **Google Public DNS** 
    *   8.8.8.8
    *   8.8.4.4
3.  **OpenDNS*** 
    *   208.67.222.222
    *   208.67.220.220

*OpenDNS does it's own version of the DNS redirection on "mistyped" entries as well, & doesn't play nice with Safari either.  I don't think there's any way around this in the free version.

That's not nearly an exhaustive list, so google "public dns servers" for more.  Choosing the best one for you is a science best left up to other software such as <a href="http://code.google.com/p/namebench/" target="_blank">namebench</a> or <a href="http://www.grc.com/dns/benchmark.htm" target="_blank">DNSBench</a>.  Either program will test among the popular public DNS servers & pick the best one for you depending on your location.

You don't *have* to have DD-WRT to use a public DNS server in your home.  If your router supports entering static DNS servers, that would be your best bet.  You can also enter it directly into your computer's network settings.

Like I mentioned above, DD-WRT has DNSMasq built in that handles all the DHCP stuff & can handle DNS requests if you want it to.  One of the nicest things about DNSMasq's DNS forwarding is that it caches your most common DNS requests.  This is a very good thing, because it makes DNS lookup times almost zero, which means websites start loading a lot quicker.  Any kind of caching you can do with DNS whether it be on your router or even a cache on your computer itself is a good thing.

Setting up DNSMasq in DD-WRT is pretty simple.  On the router web interface, go to the Basic Setup page (Setup -> Basic Setup).  Halfway down the page, modify the static DNS entries to include whichever public DNS servers you chose.  You will need to fill in all 3, otherwise a blank spot gets filled in by your ISP's DNS, which defeats the purpose.  Make sure "Use DNSMasq for DNS" is checked.

{% img /images/2011/01/dd-wrt_setup_dns.png "DD-WRT Basic Setup" %}

Once you've done that, go to the Services tab (Services -> Services).  Halfway down the page, find the DNSMasq box & configure it to look like this screenshot:

{% img /images/2011/01/dd-wrt_setup_dnsmasq.png "Setup DNSMasq" %}

You can leave "Local DNS" disabled if you don't know what it does.  Probably the most important option here is to set the **cache-size**.  By default, DNSMasq's cache-size is 150, which means it will store up to 150 entries.  That's not bad, but we can make it better.  The more cached entries, the better.  However, picking the right cache size depends entirely on your router & how much memory it has.  If it's a smaller router (like a WRT54G) & you're using a mini or micro DD-WRT build, try a conservative number like 2000.  If it's a bigger router and you're using a standard, vpn, or mega DD-WRT build, you can try 10,000 like I am doing.  They key point here is to monitor the memory usage on the Status page:

{% img /images/2011/01/dd-wrt_memory_usage.png "Memory Usage" %}

Keep an eye on this after you turn on caching.  Look at it after a few days (depending on how heavily you use the web) to see if your memory is getting full.  If it is, decrease your cache size.

Once you make these settings, reboot all of your computers & routers & modems just for good measure (or if you know how to flush their DNS caches, do that).  Your router keeps it's cache until it's rebooted, so keep that in mind each time you reboot, it's going to have to rebuild the cache.  However, the good thing about DD-WRT is that it's very stable & hardly ever requires a reboot (at least on my end).  Start visiting some of your most frequently visited websites.  The first visit, you won't notice much difference because it hasn't been cached yet.  However, the second visit & each visit after that will be faster because your router is telling your computer how to resolve the IP address of the DNS name you're going to, and that's always going to be faster than using an external DNS server.  I can definitely tell a difference in my overall browsing experience using DD-WRT's DNSMasq DNS cache.
