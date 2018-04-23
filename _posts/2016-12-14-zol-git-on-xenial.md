---
title: ZoL GIT on Xenial
tags:
- linux
- zfs
- ubuntu
- xenial
- git
categories:
- zfs
- linux
- ubuntu
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/ZoL.png
  overlay_image: /assets/ZoL.png
---

Ubuntu Xenial included ZFS by default. But for those that adventureous and seeking new features, use a ZFS on Linux (ZoL) fresh from GIT.

# Removing the old

## Unload Kernel

```console
sudo rmmod zfs
sudo rmmod spl
```

Just make sure they are not in use. No ZFS pool activated.

## Removing old driver

Remove the old from default kernel:

```console
rm -rf /lib/modules/$(uname -r)/kernel/zfs/
```

# Dependencies

```console
apt -y install build-essential autoconf libtool gawk alien fakeroot linux-headers-$(uname -r)
apt -y install zlib1g-dev uuid-dev libattr1-dev libblkid-dev libselinux-dev libudev-dev
apt -y install parted lsscsi ksh
apt -y install autoconf git libdevmapper-dev
```

# ZFS

We just want the _kernel_ because the userspace tool from Ubuntu is sufficient for now.

Let's download the sources:

```console
git clone https://github.com/zfsonlinux/spl
git clone https://github.com/zfsonlinux/zfs
```

## SPL Kernel

Go:

```console
cd spl
```

Do the _stanza:_

```console
./autogen.sh
./configure --prefix=/usr --with-config=kernel
make -j$(nproc)
sudo make install
```

## ZFS Kernel

Go:

```console
cd ../zfs
```

Do the _stanza:_

```console
./autogen.sh
./configure --prefix=/usr --with-config=kernel
make -j$(nproc)
sudo make install
```

# Done

We can restart for better, or we can reload:

```console
sudo modprobe zfs
```

# IFs
Sometimes life gives you lemon, find out what's wrong with making sure that you are loading the right kernel

```console
sudo modinfo zfs
```

This made me frustrated in the past. I just realized at some point that the kernel was still in bed with the old ZFS kernel module.
