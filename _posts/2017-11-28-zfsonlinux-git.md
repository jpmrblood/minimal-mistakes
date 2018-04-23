---
title: ZFSonLinux GIT on Ubuntu 16.04
tags:
  - zfs
  - ubuntu
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/ZoL.png
  overlay_image: /assets/ZoL.png
excerpt: For every ZoL git pull, add ./autogen.sh
---

```bash
 export LINUX_VERSION=4.10.0-41-generic
 export LINUX_PATH=/usr/src/linux-headers-$LINUX_VERSION
```

# SPL

```bash
cd spl

make clean

git pull

./autogen.sh

./configure --prefix=/usr --disable-static --with-gnu-ld --with-linux=$LINUX_PATH --with-linux-obj=$LINUX_PATH --libexecdir=/usr/lib/zfs-linux --bindir=/bin --sbindir=/sbin --localstatedir=/var --runstatedir=/run --sysconfdir=/etc --with-config=kernel

make -j$(nproc)

sudo make install

```

# ZFS

```bash
cd ../zfs

make clean

git pull

./autogen.sh

./configure --prefix=/usr --disable-static --with-gnu-ld --with-linux=$LINUX_PATH --with-linux-obj=$LINUX_PATH --libexecdir=/usr/lib/zfs-linux --bindir=/bin --sbindir=/sbin --localstatedir=/var --runstatedir=/run --sysconfdir=/etc --with-config=kernel

make -j$(nproc)

sudo make install
```
