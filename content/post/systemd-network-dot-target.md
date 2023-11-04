+++
title = "Systemd Network Dot Target"
date = "2016-08-30"
slug = "2016/08/30/systemd-network-dot-target"
Categories = []
+++

This was somewhat of a shocker and I fully acknowledge I may be missing some info here during my limited 2 day research debugging why an app was binding to localhost instead of waiting for DHCP to do it's thing even though it had `After=network.target` defined in it's systemd service file.

<!-- more -->

According to [this post](https://www.freedesktop.org/wiki/Software/systemd/NetworkTarget/), you need to be using a network management tool that's systemd aware, it seems.  The article lists two, **NetworkManager** & **systemd-networkd**.  However, Debian 8 Jessie's default network manager is still **ifupdown** where you configure `/etc/network/interfaces`.  You can use another, but that's the one that's there by default according to [their wiki](https://wiki.debian.org/NetworkConfiguration).

The problem there is that many systemd services requiring network.target will not work with **ifupdown**.  It's not systemd aware, or should I say, systemd is not aware of it.  I didn't have this issue unless I was configuring my server to use DHCP (which I rarely need to do).  If it was a static IP, the service I was testing (freeswitch) seemed to come up fine.  However, I think that's just a race condition where the network just happens to win every time.

So, I switched to using **systemd-networkd** on these few servers & it seems to have been working well so far.  I didn't like initially how it seems to take over the stub resolver but that seems to be the way it works.

Some notes on how to set it up:

#####Configure the interface
{% codeblock Terminal %}
cat /etc/systemd/network/wired.network 
[Match]
Name=eth0

[Network]
DHCP=yes
{% endcodeblock %}

#####Enable the necessary systemd services
{% codeblock Terminal %}
systemctl enable systemd-networkd.service
systemctl enable systemd-resolved.service
systemctl enable systemd-networkd-wait-online.service
{% endcodeblock %}

#####Symlink resolv.conf
*This is required if you want to use the DHCP assigned DNS servers*
{% codeblock Terminal %}
ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf
{% endcodeblock %}

Make sure to comment out eth0 in `/etc/network/interfaces`, then reboot the server to confirm everything comes up OK.

#####Misc
I'm surprised this hasn't made more noise than it already has.  I guess DHCP isn't that common on linux servers.

I also got a chuckle out of the end of the FreeDesktop article:
>If you are a developer, instead of wondering what to do about `network.target`, please just fix your program to be friendly to dynamically changing network configuration. That way you will make your users happy because things just start to work, and you will get fewer bug reports as your stuff is just rock solid. You also make the boot faster for your users, as they don't have to delay arbitrary services for the network anymore (which is particularly annoying for folks with slow address assignment replies from a DHCP server).
