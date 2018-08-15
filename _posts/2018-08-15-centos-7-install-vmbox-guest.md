---
title: CentOS 7 Install VMBOX Guest
tags:
  - VirtualBox
  - CentOS
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Installing VMBOX Guest Addition in CentOS 7 Network Install.
---

Install prequisite packages first:

```sh
yum install perl gcc dkms kernel-headers bzip2 make kernel-devel kernel-devel-`uname -r`
```

Then run the VMBOX guest installer:
```sh
mount -r /dev/cdrom /mnt
/mnt/VBoxLinuxAdditions.run
```

Restart and be done with it.