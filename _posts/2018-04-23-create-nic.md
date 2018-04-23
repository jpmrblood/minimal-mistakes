---
title: Create NIC in VMBOX
tags:
  - nic
  - guest
  - vm
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Create NIC in VMBOX
---
```bash
sudo tee /etc/network/interfaces.d/enp0s8 << EOF
auto enp0s8
allow-hotplug enp0s8
iface enp0s8 inet static
  address 192.0.2.11
  netmask 255.255.255.0
EOF
```
