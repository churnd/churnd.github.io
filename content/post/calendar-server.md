+++
title = "Calendar Server"
Categories = []
+++
I have been searching far and wide for a decent cross-platform calendar server that&#8217;s CalDAV compatible. We use Groupwise at work, which is great for Windows clients.  Anyone who&#8217;s used the Mac and Linux client knows that it&#8217;s just not a good experience.  There are several features offered in the Windows client that are lacking in OS X and Linux.  Does anyone else find that odd considering Groupwise is a Novell product?  There IS the SOAP port possibility, but the Groupwise admins refuse to open it for reasons I&#8217;m not aware of. <div>
</div>

<div>
  Anyway, Here&#8217;s a few I&#8217;ve found: <div>
  </div>
  
  <div>
    <span class="Apple-style-span" style="font-weight:bold;">Free</span>: <ol>
      <li>
        <a href="http://trac.calendarserver.org/projects/calendarserver">Darwin Calendar Server</a> &#8211; this is the same exact (actually newer) server as what Apple offers on OS X Leopard Server, sans the GUI.  It&#8217;s python based, and the Wiki contains the basic stuff you need to know to get it up and running.
      </li>
      <li>
        <a href="http://chandlerproject.org/Projects/CosmoHome">Cosmo Calendar Server</a> &#8211; part of the <a href="http://chandlerproject.org/">Chandler project</a>.  It&#8217;s java based, and looks promising.  Last I looked into it, it was very early alpha.  It seems to have made a bit of progress since then.  Now it seems to offer an all around solution:  a client and server, as well as a free (for now) hosted server called <a href="http://hub.chandlerproject.org">Chandler Hub</a>.
      </li>
      <li>
        <a href="http://www.bedework.org/bedework/">Bedework</a> - a calendar server also built on java with CalDAV support.  We tried setting this up in our offices once, but Tomcat kept crashing.  I might try again from source.
      </li>
      <li>
        <a href="http://rscds.sourceforge.net/">DAViCal</a> &#8211; another CalDAV server.  I haven&#8217;t tried it out because I&#8217;m not very proficient with PostgreSQL.
      </li>
      <li>
        <a href="http://www.zimbra.com/">Zimbra</a> &#8211; A bit overkill for someone looking for just a calendar server, but it&#8217;ll get the job done with a web interface and CalDAV support.
      </li>
    </ol>
    
    <div>
      <span class="Apple-style-span" style="font-weight:bold;">Non-Free</span>:
    </div>
    
    <div>
      <ol>
        <li>
          <a href="http://www.apple.com/server/macosx/">OS X 10.5 Server</a> &#8211; Much more than a calendar server, but it&#8217;ll get the job done.  Basically gives you a GUI to Darwin Calendar Server, I think.
        </li>
        <li>
          <a href="http://www.nowsoftware.com/nighthawkSubsite/index.html">Nighthawk</a> &#8211; One of my top choices for a commercial calendar server and client.  It&#8217;s not available yet, but from what I&#8217;ve seen it will be fantastic.
        </li>
      </ol>
      
      <div>
      </div>
      
      <div>
        In a perfect world, everyone would use iCal so I could deploy <a href="http://www.busymac.com/">BusySync</a>, which I use myself for my personal calendar and is nothing short of phenomenal.  It&#8217;s great for LAN calendar sharing, as well as it&#8217;s ability to tie into Google Calendar.
      </div>
      
      <div>
      </div>
      
      <div>
        I considered using Google Calendar as a calendar server for my group at work, but the fact that it was not internal to our organization doesn&#8217;t sit well with me.
      </div>
      
      <div>
      </div>
      
      <div>
        If you know of anything I haven&#8217;t listed here (not Exchange!!), please let me know!
      </div>
    </div>
  </div>
</div>
