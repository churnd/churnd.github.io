+++
title = "MacPorts Update Script"
Categories = []
+++
I just got tired of typing each command in manually every time, so I just put them in a shell script:

<pre class="lang:default decode:true ">#!/bin/bash
if [ "$(whoami)" != 'root' ]; then
echo "You have no permission to run $0 as non-root user."
exit 1
fi

export PATH=/opt/local/bin:/opt/local/sbin:$PATH

port selfupdate
port -d sync
port upgrade outdated
port clean --all installed &gt;&gt; /dev/null 2&gt;&1
port uninstall inactive</pre>

&nbsp;

<!--more-->

The last two are just because I don&#8217;t like &#8220;extra junk&#8221; building up on my systems & by default <a class="zem_slink" title="MacPorts" href="http://www.macports.org/" rel="homepage">MacPorts</a> doesn&#8217;t remove previous versions or clean up after itself.

You can save the script, make it executable, & put it somewhere in your path so when you&#8217;re ready to update MacPorts, you can just type &#8220;*sudo <script_name>*&#8221; & watch it go.

I also considered scheduling this, but in my experience it doesn&#8217;t always finish successfully (usually due to a bad download of the sourcecode), so the process needs to be monitored while it&#8217;s happening.  Otherwise, you could eventually wind up with a broken ports collection.
