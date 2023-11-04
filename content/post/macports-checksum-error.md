+++
title = "MacPorts Checksum Error"
Categories = []
+++
This has a tendency to happen when using MacPorts:

{% codeblock %}
$ sudo port upgrade outdated
---> Computing dependencies for curl-ca-bundle
---> Fetching curl-ca-bundle
---> Attempting to fetch curl-7.21.2.tar.bz2 from http://curl.sourceforge.net/download/
---> Attempting to fetch certdata-1.70.txt from http://mxr.mozilla.org/mozilla/source/security/nss/lib/ckfw/builtins/certdata.txt?raw=1&dummy=
---> Verifying checksum(s) for curl-ca-bundle
Error: Checksum (sha1) mismatch for curl-7.21.2.tar.bz2
Error: Checksum (rmd160) mismatch for curl-7.21.2.tar.bz2
Error: Target org.macports.checksum returned: Unable to verify file checksums
Log for curl-ca-bundle is at: /opt/local/var/macports/logs/_opt_local_var_macports_sources_rsync.macports.org_release_ports_net_curl-ca-bundle/main.log
Error: Unable to upgrade port: 1
To report a bug, see http://guide.macports.org/#project.tickets>
{% endcodeblock %}

<!--more-->

I manage several different machines that use MacPorts for a few unix programs, and I keep seeing them choke on **curl-ca-bundle**. If you go to <a href="http://curl.sourceforge.net" target="_blank">curl.sourceforge.net</a>, it redirects to <a href="http://curl.haxx.se" target="_blank">curl.haxx.se</a> (which does look awfully suspicious). Not sure exactly why the download keeps failing to pass it's checksum, but the only way I've found to resolve the issue is to clean up & keep trying:

{% codeblock %}
$ sudo port clean --all installed
---> Cleaning atk
---> Cleaning autoconf
---> Cleaning automake
.....
--snip-->
.....
---> Cleaning xorg-xproto
---> Cleaning xorg-xtrans
---> Cleaning xrender
---> Cleaning zlib
$ sudo port clean --all curl-ca-bundle
---> Cleaning curl-ca-bundle</pre>
{% endcodeblock %}

Then run

{% codeblock %}
sudo port upgrade outdated
{% endcodeblock %}

until it works.

\*\* Update \*\*

Got a reply on Twitter <a href="http://twitter.com/#!/macports/status/11056609077755905" target="_blank">from @Macports</a>:

> @churnd See also <a href="http://trac.macports.org/wiki/FAQ#checksums" target="_blank">http://trac.macports.org/wiki/FAQ#checksums</a>

More useful info on what's actually happening.
