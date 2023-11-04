+++
title = "Opensolaris 2009 6 in Vmware Fusion"
Categories = []
+++
To install vmware-tools:

> ln -s <span style="margin:0;padding:0;"><em>/usr/lib/vmware-tools/configurator/XOrg/</em><span style="margin:0;padding:0;"><em>7.1</em> <span style="margin:0;padding:0;"><em>/usr/lib/vmware-tools/configurator/XOrg/</em><span style="margin:0;padding:0;"><em>7.4</em></span></span></span></span>

or if you&#8217;re using 64-bit:

> ln -s <span style="margin:0;padding:0;"><em>/usr/lib/vmware-tools/configurator/XOrg/</em><span style="margin:0;padding:0;"><em>7.1_x64<span style="font-style:normal;"> </span></em><span style="margin:0;padding:0;"><em>/usr/lib/vmware-tools/configurator/XOrg/</em><span style="margin:0;padding:0;"><em>7.4</em></span></span></span></span>

*<span style="font-style:normal;">Taken from here:  <a href="http://communities.vmware.com/thread/212833" target="_blank">http://communities.vmware.com/thread/212833</a></span>*

<span style="margin:0;padding:0;"><span style="margin:0;padding:0;"><span style="margin:0;padding:0;"><span style="margin:0;padding:0;"><em>**Edit**</em></span></span></span></span>

*<span style="font-style:normal;">This fixes the installation problem, but the tools themselves still do not work properly.  I haven&#8217;t found any other solution yet.  I&#8217;m going to try open-vm-tools next.</span>*
