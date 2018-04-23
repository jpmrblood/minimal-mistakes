---
title: Install Steam
tags:
  - ubuntu
  - steam
  - linux
categories:
  - tips
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2016/12/steam.jpg
  overlay_image: /assets/2016/12/steam.jpg
excerpt: "Instaling Steam with better gaming experience."
---
Installing Steam with better gaming experience.


# Add i386 Architecture

```console
$ sudo dpkg --add-architecture i386
$ sudo apt-get update
```

# F The Software Patent (Not In My Country)

```console
$ sudo apt-get remove --purge libtxc-dxtn-s2tc0
$ wget https://launchpad.net/~xorg-edgers/+archive/ubuntu/ppa/+files/libtxc-dxtn0_1.0.1-0.3ubuntu0sarvatt+raring_amd64.deb
$ wget https://launchpad.net/~xorg-edgers/+archive/ubuntu/ppa/+files/libtxc-dxtn0_1.0.1-0.3ubuntu0sarvatt+raring_i386.deb
$ sudo dpkg -i *.deb
$ sudo apt-get -f install
```

# Install Steam

```console
$ sudo apt-get install steam
```

Done.
