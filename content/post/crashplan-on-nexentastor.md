+++
title = "Crashplan on Nexentastor"
Categories = []
+++

Following up on my last post, [Netatalk on NexentaStor](http://churnd.net/2013/02/11/netatalk-3-afp-on-nexentastor/ "Netatalk 3 (AFP) on NexentaStor - #!"), I mentioned there that I only use Time Machine for "bare metal" type backups.  As in if I need to restore something specific to the OS itself, or reload the OS in event of a hardware failure.  I use <a title="CrashPlan" href="http://www.crashplan.com" target="_blank" rel="homepage">CrashPlan</a> for all my actual data backups, because I think it's superior to Time Machine.  For why I think that, check out the <a href="http://www.crashplan.com/consumer/details.html" target="_blank">details</a>.  I've also had Time Machine crap out on me more than once when the disk gets full & tries to expire too much data, the only solution being to wipe the drive & start backups over.  Not cool.  Never had that problem with CrashPlan.

<!--more-->

<a title="Code 42 Software" href="http://www.crashplan.com" target="_blank" rel="homepage">Crashplan</a> is also the only backup solution I know of that is really cross-platform & allows free local backups.  They support Windows, Mac, Linux, & Solaris, & state that FreeBSD support is coming.  Can't beat that.  I will say though, this is not supported by Crashplan or NexentaStor.  Installing it requires some workarounds because Nexenta uses apt as it's underlying package management tool, whereas Crashplan is a pkg type installer. There are other ways to install it besides this one, but I like this one better because other ways I've read involve mixing the Crashplan Linux & Solaris installers.  In reality, that may be just fine since Crashplan is mostly a java app, but still&#8230; I want 100% Solaris if I can get it. So this install is a two step process, & takes a little longer.  It involves setting up an OpenIndiana VM, installing Crashplan to that, then copying the files over to NexentaStor.  Simple enough, right?  I'm assuming you have working OpenIndiana & NexentaStor instances & that you can ssh between each as root. To install Crashplan on OpenIndiana, it's pretty straightforward:

1.  Make sure it has java installed: ````pkg install jdk````
2.  Download the Solaris installer from Crashplan.com & untar to /tmp
3.  Install it: ````cd /tmp && pkgadd -d .````
4.  The install process shows you everything you need to know, but in case you didn't copy it down:

{% codeblock Terminal %}Installing CrashPlan as <CrashPlan>

## Executing preinstall script.
## Installing part 1 of 1.
/opt/sfw/crashplan/bin/CrashPlan.desktop
/opt/sfw/crashplan/bin/CrashPlanDesktop
/opt/sfw/crashplan/bin/CrashPlanEngine
/opt/sfw/crashplan/bin/crashplan.xml
/opt/sfw/crashplan/bin/restart_solaris.sh
/opt/sfw/crashplan/bin/run.conf
/opt/sfw/crashplan/client-build.properties
/opt/sfw/crashplan/conf/custom_sample.properties
/opt/sfw/crashplan/conf/default.service.xml
/opt/sfw/crashplan/conf/service.log.properties
/opt/sfw/crashplan/conf/ui.log.properties
/opt/sfw/crashplan/conf/ui.properties
/opt/sfw/crashplan/conf/upgradeui.log.properties
/opt/sfw/crashplan/conf/upgradeui.properties
/opt/sfw/crashplan/doc/EULA
/opt/sfw/crashplan/doc/readme.html
/opt/sfw/crashplan/doc/readme.odt
/opt/sfw/crashplan/doc/readme.pdf
/opt/sfw/crashplan/doc/readme.rtf
/opt/sfw/crashplan/installer/solaris/.defaults
/opt/sfw/crashplan/installer/solaris/EULA
/opt/sfw/crashplan/jniwrap.lic
/opt/sfw/crashplan/lang/txt.properties
/opt/sfw/crashplan/lang/txt_ca.properties
/opt/sfw/crashplan/lang/txt_da.properties
/opt/sfw/crashplan/lang/txt_de.properties
/opt/sfw/crashplan/lang/txt_en.properties
/opt/sfw/crashplan/lang/txt_es.properties
/opt/sfw/crashplan/lang/txt_es_AR.properties
/opt/sfw/crashplan/lang/txt_es_ES.properties
/opt/sfw/crashplan/lang/txt_es_MX.properties
/opt/sfw/crashplan/lang/txt_fi.properties
/opt/sfw/crashplan/lang/txt_fr.properties
/opt/sfw/crashplan/lang/txt_hu.properties
/opt/sfw/crashplan/lang/txt_it.properties
/opt/sfw/crashplan/lang/txt_ja.properties
/opt/sfw/crashplan/lang/txt_nl.properties
/opt/sfw/crashplan/lang/txt_no.properties
/opt/sfw/crashplan/lang/txt_pl.properties
/opt/sfw/crashplan/lang/txt_pt.properties
/opt/sfw/crashplan/lang/txt_pt_BR.properties
/opt/sfw/crashplan/lang/txt_sv.properties
/opt/sfw/crashplan/lang/txt_th.properties
/opt/sfw/crashplan/lang/txt_tr.properties
/opt/sfw/crashplan/lang/txt_zh.properties
/opt/sfw/crashplan/lang/txt_zh_TW.properties
/opt/sfw/crashplan/lib/c42_protolib.jar
/opt/sfw/crashplan/lib/com.backup42.desktop.jar
/opt/sfw/crashplan/lib/com.jniwrapper.jniwrap.jar
/opt/sfw/crashplan/lib/com.jniwrapper.macpack.jar
/opt/sfw/crashplan/lib/com.jniwrapper.winpack.jar
/opt/sfw/crashplan/lib/commons-collections-3.2.1-mini.jar
/opt/sfw/crashplan/lib/commons-jxpath-1.1.jar
/opt/sfw/crashplan/lib/jna-3.2.5.jar
/opt/sfw/crashplan/lib/json-20070829.jar
/opt/sfw/crashplan/lib/json-lib-2.4.jar
/opt/sfw/crashplan/lib/jtux.jar
/opt/sfw/crashplan/lib/log4j-1.2.16.jar
/opt/sfw/crashplan/lib/miglayout15-swt.jar
/opt/sfw/crashplan/lib/org.eclipse.core.commands_3.6.1.v20120814-150512.jar
/opt/sfw/crashplan/lib/org.eclipse.equinox.common_3.6.100.v20120522-1841.jar
/opt/sfw/crashplan/lib/org.eclipse.jface_3.8.101.v20120817-083647.jar
/opt/sfw/crashplan/lib/org.eclipse.osgi_3.8.1.v20120830-144521.jar
/opt/sfw/crashplan/lib/protobuf-java-2.4.1.jar
/opt/sfw/crashplan/lib/rhino-1.7r3.jar
/opt/sfw/crashplan/lib/sbbi-upnplib-1.0.4.jar
/opt/sfw/crashplan/lib/slf4j-api-1.6.1.jar
/opt/sfw/crashplan/lib/slf4j-log4j12-1.6.1.jar
/opt/sfw/crashplan/lib/swt.jar
/opt/sfw/crashplan/lib/trove-3.0.2.jar
/opt/sfw/crashplan/lib/twitter4j.jar
/opt/sfw/crashplan/libjtux.so
/opt/sfw/crashplan/skin/icon_app_128x128.png
/opt/sfw/crashplan/skin/icon_app_16x16.png
/opt/sfw/crashplan/skin/icon_app_32x32.png
/opt/sfw/crashplan/skin/icon_app_64x64.png
/opt/sfw/crashplan/skin/logo_main.png
/opt/sfw/crashplan/skin/skin.properties
/opt/sfw/crashplan/skin/splash_default.png
/opt/sfw/crashplan/skin/splash_plus.png
/opt/sfw/crashplan/skin/window_bg.jpg
/opt/sfw/crashplan/upgrade/start.bat
/opt/sfw/crashplan/upgrade/start.sh
/opt/sfw/crashplan/upgrade/startDesktop.bat
/opt/sfw/crashplan/upgrade/startDesktop.sh
/opt/sfw/crashplan/upgrade/startDesktopLinux.sh
/opt/sfw/crashplan/upgrade/startDesktopSolaris.sh
/opt/sfw/crashplan/upgrade/startFirst.sh
/opt/sfw/crashplan/upgrade/startLinux.sh
/opt/sfw/crashplan/upgrade/startSolaris.sh
[ verifying class <none> ]
## Executing postinstall script.
log dir: /opt/sfw/crashplan/log
mkdir: /opt/sfw/crashplan/log: [File exists]

adjusting service xml paths
adjusting manifest path
creating identity path

CrashPlan has been installed.

Important directories:
Installation:
/opt/sfw/crashplan
Logs:
/opt/sfw/crashplan/log
Default archive location:
/opt/sfw/var/crashplan

Start Script (run as root):
/opt/sfw/crashplan/bin/CrashPlanEngine start|stop

Start Desktop UI:
/opt/sfw/crashplan/bin/CrashPlanDesktop

You may connect a remote Desktop UI to this Service via port-forwarding
and manage it remotely. Instructions for remote management are in the
readme files placed in your installation directory:
/opt/sfw/crashplan/doc

To enable CrashPlan as a service (as root):
/usr/sbin/svccfg import /opt/sfw/crashplan/bin/crashplan.xml
/usr/sbin/svcadm enable crashplan

Thank you for installing CrashPlan for Solaris.

Installation of CrashPlan was successful.{% endcodeblock %}

Notice the last step details how to import Crashplan's SMF manifest, so you can manage the service in true Solaris form.  You don't have to do that on OpenIndiana, but no harm in doing so at this point. Now we want to get all that stuff over to NexentaStor, so as root:

{% codeblock Terminal %}#rsync -av --progress /opt/sfw nexentastor:/opt/{% endcodeblock %}

README VERY IMPORTANT:  this assumes there is no /opt/sfw on your NexentaStor install already!!  It's a pretty safe bet as NexentaStor doesn't install anything there, but please make sure yourself.  Also replace "nexentastor" with the name of your NexentaStor server, or it's IP.  Enter the root password & it'll do it's thing.  You should see each item it copies print out to the screen:

{% codeblock Terminal %}# rsync -av --progress /opt/ nexentastor:/opt/
Password: 
sending incremental file list
./
sfw/
sfw/crashplan/
sfw/crashplan/client-build.properties
171 100% 0.43kB/s 0:00:00 (xfer#775, to-check=102/1161)
sfw/crashplan/install.vars
154 100% 0.39kB/s 0:00:00 (xfer#776, to-check=101/1161)
sfw/crashplan/jniwrap.lic
330 100% 0.83kB/s 0:00:00 (xfer#777, to-check=100/1161)
sfw/crashplan/libjtux.so
72762 100% 38.14MB/s 0:00:00 (xfer#778, to-check=99/1161)
sfw/crashplan/bin/
sfw/crashplan/bin/CrashPlan.desktop
290 100% 283.20kB/s 0:00:00 (xfer#779, to-check=89/1161)
sfw/crashplan/bin/CrashPlanDesktop
307 100% 299.80kB/s 0:00:00 (xfer#780, to-check=88/1161)
sfw/crashplan/bin/CrashPlanEngine
1508 100% 1.44MB/s 0:00:00 (xfer#781, to-check=87/1161)
sfw/crashplan/bin/crashplan.xml
1858 100% 1.77MB/s 0:00:00 (xfer#782, to-check=86/1161)
sfw/crashplan/bin/restart_solaris.sh
862 100% 841.80kB/s 0:00:00 (xfer#783, to-check=85/1161)
sfw/crashplan/bin/run.conf
479 100% 467.77kB/s 0:00:00 (xfer#784, to-check=84/1161)
sfw/crashplan/conf/
sfw/crashplan/conf/custom_sample.properties
3368 100% 3.21MB/s 0:00:00 (xfer#785, to-check=83/1161)
sfw/crashplan/conf/default.service.xml
872 100% 851.56kB/s 0:00:00 (xfer#786, to-check=82/1161)
sfw/crashplan/conf/service.log.properties
750 100% 732.42kB/s 0:00:00 (xfer#787, to-check=81/1161)
sfw/crashplan/conf/ui.log.properties
467 100% 456.05kB/s 0:00:00 (xfer#788, to-check=80/1161)
sfw/crashplan/conf/ui.properties
277 100% 135.25kB/s 0:00:00 (xfer#789, to-check=79/1161)
sfw/crashplan/conf/upgradeui.log.properties
1013 100% 494.63kB/s 0:00:00 (xfer#790, to-check=78/1161)
sfw/crashplan/conf/upgradeui.properties
44 100% 21.48kB/s 0:00:00 (xfer#791, to-check=77/1161)
sfw/crashplan/doc/
sfw/crashplan/doc/EULA
44099 100% 21.03MB/s 0:00:00 (xfer#792, to-check=76/1161)
sfw/crashplan/doc/readme.html
16041 100% 5.10MB/s 0:00:00 (xfer#793, to-check=75/1161)
sfw/crashplan/doc/readme.odt
69754 100% 16.63MB/s 0:00:00 (xfer#794, to-check=74/1161)
sfw/crashplan/doc/readme.pdf
40088 100% 7.65MB/s 0:00:00 (xfer#795, to-check=73/1161)
sfw/crashplan/doc/readme.rtf
41636 100% 6.62MB/s 0:00:00 (xfer#796, to-check=72/1161)
sfw/crashplan/installer/
sfw/crashplan/installer/solaris/
sfw/crashplan/installer/solaris/.defaults
83 100% 11.58kB/s 0:00:00 (xfer#797, to-check=70/1161)
sfw/crashplan/installer/solaris/EULA
44099 100% 4.67MB/s 0:00:00 (xfer#798, to-check=69/1161)
sfw/crashplan/lang/
sfw/crashplan/lang/txt.properties
74570 100% 6.47MB/s 0:00:00 (xfer#799, to-check=68/1161)
sfw/crashplan/lang/txt_ca.properties
83061 100% 6.09MB/s 0:00:00 (xfer#800, to-check=67/1161)
sfw/crashplan/lang/txt_da.properties
73754 100% 5.02MB/s 0:00:00 (xfer#801, to-check=66/1161)
sfw/crashplan/lang/txt_de.properties
82420 100% 4.91MB/s 0:00:00 (xfer#802, to-check=65/1161)
sfw/crashplan/lang/txt_en.properties
288 100% 17.58kB/s 0:00:00 (xfer#803, to-check=64/1161)
sfw/crashplan/lang/txt_es.properties
82806 100% 4.39MB/s 0:00:00 (xfer#804, to-check=63/1161)
sfw/crashplan/lang/txt_es_AR.properties
81945 100% 3.91MB/s 0:00:00 (xfer#805, to-check=62/1161)
sfw/crashplan/lang/txt_es_ES.properties
80929 100% 3.51MB/s 0:00:00 (xfer#806, to-check=61/1161)
sfw/crashplan/lang/txt_es_MX.properties
69105 100% 2.87MB/s 0:00:00 (xfer#807, to-check=60/1161)
sfw/crashplan/lang/txt_fi.properties
79646 100% 3.04MB/s 0:00:00 (xfer#808, to-check=59/1161)
sfw/crashplan/lang/txt_fr.properties
84919 100% 3.00MB/s 0:00:00 (xfer#809, to-check=58/1161)
sfw/crashplan/lang/txt_hu.properties
89918 100% 2.96MB/s 0:00:00 (xfer#810, to-check=57/1161)
sfw/crashplan/lang/txt_it.properties
75391 100% 2.32MB/s 0:00:00 (xfer#811, to-check=56/1161)
sfw/crashplan/lang/txt_ja.properties
130198 100% 3.65MB/s 0:00:00 (xfer#812, to-check=55/1161)
sfw/crashplan/lang/txt_nl.properties
73500 100% 2.00MB/s 0:00:00 (xfer#813, to-check=54/1161)
sfw/crashplan/lang/txt_no.properties
73788 100% 1.90MB/s 0:00:00 (xfer#814, to-check=53/1161)
sfw/crashplan/lang/txt_pl.properties
80730 100% 1.97MB/s 0:00:00 (xfer#815, to-check=52/1161)
sfw/crashplan/lang/txt_pt.properties
75719 100% 1.76MB/s 0:00:00 (xfer#816, to-check=51/1161)
sfw/crashplan/lang/txt_pt_BR.properties
79742 100% 1.81MB/s 0:00:00 (xfer#817, to-check=50/1161)
sfw/crashplan/lang/txt_sv.properties
79567 100% 1.72MB/s 0:00:00 (xfer#818, to-check=49/1161)
sfw/crashplan/lang/txt_th.properties
208127 100% 4.05MB/s 0:00:00 (xfer#819, to-check=48/1161)
sfw/crashplan/lang/txt_tr.properties
89075 100% 1.67MB/s 0:00:00 (xfer#820, to-check=47/1161)
sfw/crashplan/lang/txt_zh.properties
92387 100% 1.66MB/s 0:00:00 (xfer#821, to-check=46/1161)
sfw/crashplan/lang/txt_zh_TW.properties
91989 100% 1.57MB/s 0:00:00 (xfer#822, to-check=45/1161)
sfw/crashplan/lib/
sfw/crashplan/lib/c42_protolib.jar
1290808 100% 389.42kB/s 0:00:03 (xfer#823, to-check=44/1161)
sfw/crashplan/lib/com.backup42.desktop.jar
5716574 100% 606.34kB/s 0:00:09 (xfer#824, to-check=43/1161)
sfw/crashplan/lib/com.jniwrapper.jniwrap.jar
215243 100% 4.89MB/s 0:00:00 (xfer#825, to-check=42/1161)
sfw/crashplan/lib/com.jniwrapper.macpack.jar
1285054 100% 418.31kB/s 0:00:03 (xfer#826, to-check=41/1161)
sfw/crashplan/lib/com.jniwrapper.winpack.jar
706581 100% 21.74MB/s 0:00:00 (xfer#827, to-check=40/1161)
sfw/crashplan/lib/commons-collections-3.2.1-mini.jar
24481 100% 771.20kB/s 0:00:00 (xfer#828, to-check=39/1161)
sfw/crashplan/lib/commons-jxpath-1.1.jar
268794 100% 6.93MB/s 0:00:00 (xfer#829, to-check=38/1161)
sfw/crashplan/lib/jna-3.2.5.jar
946973 100% 9.82MB/s 0:00:00 (xfer#830, to-check=37/1161)
sfw/crashplan/lib/json-20070829.jar
41829 100% 8.64MB/s 0:00:00 (xfer#831, to-check=36/1161)
sfw/crashplan/lib/json-lib-2.4.jar
159123 100% 25.29MB/s 0:00:00 (xfer#832, to-check=35/1161)
sfw/crashplan/lib/jtux.jar
41291 100% 5.63MB/s 0:00:00 (xfer#833, to-check=34/1161)
sfw/crashplan/lib/log4j-1.2.16.jar
481534 100% 24.17MB/s 0:00:00 (xfer#834, to-check=33/1161)
sfw/crashplan/lib/miglayout15-swt.jar
69028 100% 3.13MB/s 0:00:00 (xfer#835, to-check=32/1161)
sfw/crashplan/lib/org.eclipse.core.commands_3.6.1.v20120814-150512.jar
108731 100% 4.51MB/s 0:00:00 (xfer#836, to-check=31/1161)
sfw/crashplan/lib/org.eclipse.equinox.common_3.6.100.v20120522-1841.jar
106763 100% 4.07MB/s 0:00:00 (xfer#837, to-check=30/1161)
sfw/crashplan/lib/org.eclipse.jface_3.8.101.v20120817-083647.jar
1090959 100% 20.81MB/s 0:00:00 (xfer#838, to-check=29/1161)
sfw/crashplan/lib/org.eclipse.osgi_3.8.1.v20120830-144521.jar
1396459 100% 219.43kB/s 0:00:06 (xfer#839, to-check=28/1161)
sfw/crashplan/lib/protobuf-java-2.4.1.jar
450279 100% 13.42MB/s 0:00:00 (xfer#840, to-check=27/1161)
sfw/crashplan/lib/rhino-1.7r3.jar
1122370 100% 17.55MB/s 0:00:00 (xfer#841, to-check=26/1161)
sfw/crashplan/lib/sbbi-upnplib-1.0.4.jar
81591 100% 1.26MB/s 0:00:00 (xfer#842, to-check=25/1161)
sfw/crashplan/lib/slf4j-api-1.6.1.jar
25496 100% 0.00kB/s 0:00:00 (xfer#843, to-check=24/1161)
sfw/crashplan/lib/slf4j-log4j12-1.6.1.jar
9753 100% 9.30MB/s 0:00:00 (xfer#844, to-check=23/1161)
sfw/crashplan/lib/swt.jar
1641584 100% 42.31MB/s 0:00:00 (xfer#845, to-check=22/1161)
sfw/crashplan/lib/trove-3.0.2.jar
2522902 100% 801.23kB/s 0:00:03 (xfer#846, to-check=21/1161)
sfw/crashplan/lib/twitter4j.jar
284059 100% 6.45MB/s 0:00:00 (xfer#847, to-check=20/1161)
sfw/crashplan/log/
sfw/crashplan/skin/
sfw/crashplan/skin/icon_app_128x128.png
9576 100% 217.48kB/s 0:00:00 (xfer#848, to-check=19/1161)
sfw/crashplan/skin/icon_app_16x16.png
813 100% 18.46kB/s 0:00:00 (xfer#849, to-check=18/1161)
sfw/crashplan/skin/icon_app_32x32.png
2099 100% 47.67kB/s 0:00:00 (xfer#850, to-check=17/1161)
sfw/crashplan/skin/icon_app_64x64.png
5094 100% 115.69kB/s 0:00:00 (xfer#851, to-check=16/1161)
sfw/crashplan/skin/logo_main.png
9960 100% 226.20kB/s 0:00:00 (xfer#852, to-check=15/1161)
sfw/crashplan/skin/skin.properties
56 100% 1.27kB/s 0:00:00 (xfer#853, to-check=14/1161)
sfw/crashplan/skin/splash_default.png
244581 100% 4.76MB/s 0:00:00 (xfer#854, to-check=13/1161)
sfw/crashplan/skin/splash_plus.png
244858 100% 4.25MB/s 0:00:00 (xfer#855, to-check=12/1161)
sfw/crashplan/skin/window_bg.jpg
213440 100% 64.13kB/s 0:00:03 (xfer#856, to-check=11/1161)
sfw/crashplan/upgrade/
sfw/crashplan/upgrade/start.bat
127 100% 124.02kB/s 0:00:00 (xfer#857, to-check=10/1161)
sfw/crashplan/upgrade/start.sh
174 100% 169.92kB/s 0:00:00 (xfer#858, to-check=9/1161)
sfw/crashplan/upgrade/startDesktop.bat
92 100% 89.84kB/s 0:00:00 (xfer#859, to-check=8/1161)
sfw/crashplan/upgrade/startDesktop.sh
312 100% 304.69kB/s 0:00:00 (xfer#860, to-check=7/1161)
sfw/crashplan/upgrade/startDesktopLinux.sh
135 100% 131.84kB/s 0:00:00 (xfer#861, to-check=6/1161)
sfw/crashplan/upgrade/startDesktopSolaris.sh
137 100% 133.79kB/s 0:00:00 (xfer#862, to-check=5/1161)
sfw/crashplan/upgrade/startFirst.sh
87 100% 84.96kB/s 0:00:00 (xfer#863, to-check=4/1161)
sfw/crashplan/upgrade/startLinux.sh
211 100% 206.05kB/s 0:00:00 (xfer#864, to-check=3/1161)
sfw/crashplan/upgrade/startSolaris.sh
213 100% 208.01kB/s 0:00:00 (xfer#865, to-check=2/1161)
sfw/crashplan/upgrade/UpgradeUI/
sfw/var/
sfw/var/crashplan/

sent 26794580 bytes received 17392 bytes 589274.11 bytes/sec
total size is 26730067 speedup is 1.00{% endcodeblock %}

Make sure java is installed on NexentaStor:

{% codeblock Terminal %}apt-get install sun-java6-jre{% endcodeblock %}

Lastly, run the two commands the install script shows you on NexentaStor as root:

{% codeblock Terminal %}#/usr/sbin/svccfg import /opt/sfw/crashplan/bin/crashplan.xml
#/usr/sbin/svcadm enable crashplan{% endcodeblock %}

Keep in mind you have to be in a pure root bash shell, not NMC, to do this on NexentaStor. Now verify it's running:

{% codeblock Terminal %}# svcs | grep crash
online         22:22:52 svc:/crashplan:default{% endcodeblock %}

Good!  All that's left is to configure it.  Crashplan has instructions on their site:  <a href="http://support.crashplan.com/doku.php/how_to/configure_a_headless_client" target="_blank">Configure a Headless Client</a>. The last step is to create a ZFS folder for Crashplan to store it's backups in.  This is easy enough in NexentaStor, just create a folder on the ZFS pool you want & set it up accordingly.  I have mine set to use compression, but that's it.  Crashplan does deduplication & more compression itself, so I figure that's plenty.

I vaguely recall having some problems getting Crashplan to see the /volumes directory where NexentaStor mounts it's pools & folders.  What I had to do was to disable Crashplan, go into /opt/sfw/crashplan/conf, & edit I think the my.service.xml file to include the location manually.  My memory's fuzzy on that, & I found the solution by Googling so I'd recommend doing that if you get stuck with the same problem. It'd be pretty cool to see NexentaStor create a plugin for Crashplan, where the installation would be as simple as a click & it would be managed by NMV.  Wouldn't take much, I don't think.  Maybe in v4.  ;)
