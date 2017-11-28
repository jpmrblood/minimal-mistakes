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
  overlay_image: /assets/ZoL.png
excerpt: For every ZoL git pull, add ./autogen.sh
---

```
 export LINUX_VERSION=/usr/src/linux-headers-4.14.1+
```

# SPL

```
cd spl

make clean

git pull

./autogen.sh

./configure --prefix=/usr --disable-static --with-gnu-ld --with-linux=$LINUX_VERSION --with-linux-obj=$LINUX_VERSION --libexecdir=/usr/lib/zfs-linux --bindir=/bin --sbindir=/sbin --localstatedir=/var --runstatedir=/run --sysconfdir=/etc --with-config=kernel

make -j$(nproc)

sudo make install

 ```

# ZFS

```
cd ../zfs

make clean

git pull

./autogen.sh

./configure --prefix=/usr --disable-static --with-gnu-ld --with-linux=$LINUX_VERSION --with-linux-obj=$LINUX_VERSION --libexecdir=/usr/lib/zfs-linux --bindir=/bin --sbindir=/sbin --localstatedir=/var --runstatedir=/run --sysconfdir=/etc --with-config=kernel

make -j$(nproc)

sudo make install
```
