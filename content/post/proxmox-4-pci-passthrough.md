+++
title = "Proxmox 4 Pci Passthrough"
date = "2015-09-21"
slug = "2015/09/21/proxmox-4-pci-passthrough"
Categories = []
+++

Worth noting:

Proxmox v4 Beta as of right now uses linux kernel v4. I updated my homelab to it recently & PCI passthrough (per my previous post) stopped working. Asked on the Proxmox forums & apparently an additional option is required due to the newer v4 kernel:

<!-- more -->

`hostpci0: 01:00.0,driver=vfio`

Compared to what was required before:

`hostpci0: 01:00.0`

Apparently vfio is the way to go with v4 kernels. It should be the default option once Proxmox v4 goes GM.

*Update (10/10/2015):*

This is the default in v4 GM, so the option is no longer needed.
