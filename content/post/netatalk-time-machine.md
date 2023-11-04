+++
title = "Netatalk Time Machine"
Categories = []
+++
In the past, many people have attempted to get Time Machine to back up to a linux server via netatalk. Usually this involved quite a bit of hackery, and was usually unreliable.

One of the reasons it was unreliable is because the netatalk share wouldn't present itself as a time machine destination. You had to throw a switch on your OS X client to get it to use any network share. This didn't always "just work".

As of <a href="http://netatalk.sourceforge.net/2.0/NEWS.html" target="_blank">Netatalk 2.0.5</a>, there is a "tm" option that can be used to present the share as a Time Machine destination. Problem is, most linux distros don't have 2.0.5 in their repos yet, so you'll have to compile it manually. I was able to do it on openSUSE 11.2 by configuring without the print option. For some reason, leaving that option off would fail, likely due to a dependency I didn't care to troubleshoot. I wasn't using print anyway.

So, when you compile, you'll most likely have everything in /usr/local/netatalk unless you specified other options when you configured. In there you'll have your AppleVolumes.default file that contains your shares, so you would add one like this:

{% codeblock AppleVolumes %}
/data TimeMachine allow:user cnidscheme:cdb options:usedots,tm
{% endcodeblock %}

The important part being at the option **tm**.

Restart netatalk: [sourcecode language="bash"]sudo /etc/init.d/atalk restart[/sourcecode]

You should now be able to see the share in Time Machine Preferences without any trickery. The really helpful thing is, if you ever have to do a full restore, the share will also show up when booting to the OS X DVD.

So now if you have a unix box, you can start using it for Time Machine backups. If you're planning one for some sort of NAS, I would actually recommend going with <a href="http://freenas.org" target="_blank">FreeNAS</a>, assuming all you need is a NAS. FreeNAS will do all of this for you, and leverages the power of ZFS.
