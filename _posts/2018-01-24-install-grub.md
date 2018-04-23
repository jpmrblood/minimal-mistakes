---
title: Install GRUB for ZFS
tags:
  - zfs
  - jessie
  - debian
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2018/01/GRUB.png
  overlay_image: /assets/2018/01/GRUB.png
excerpt: For every ZoL git pull, add ./autogen.sh
---

Debian Jessie failed to get ZFS root in grub-probe. It would ended up like this:

```bash
$ sudo grub-probe /
grub-probe: error: failed to get canonical path of `/dev/scsi-3600605b008b089301eb25768126fbaa6'.
```
Luckily, [Someone at askubuntu](https://askubuntu.com/a/943425) suggested to set an env:
```bash
ZPOOL_VDEV_NAME_PATH=1
```

In order to make GRUB recognize the env, we have to have newer version of GRUB.
Since GRUB is a static application that sits on our boot time, why not compile it.

For the sake of completeness, don't forget to install the necessary packages:
```bash
sudo apt-get build-dep grub-efi-amd64
```

To compile:
```bash
git clone git://git.savannah.gnu.org/grub.git
cd grub
./autgen.sh
./configure --prefix=/usr --sbindir=/sbin --sysconfdir=/etc --with-platform=efi
make -j$(nproc)
sudo make install
```

Oh, don't forget to install `efibootmgr` so that GRUB can register EFI.
```bash
sudo apt install efibootmgr
```

# The Commands

Now we can run everything well:
```bash
$ sudo ZPOOL_VDEV_NAME_PATH=1 grub-probe /
zfs
```

Install GRUB:
```bash
$ sudo ZPOOL_VDEV_NAME_PATH=1 grub-install /dev/sda
```

Done.
