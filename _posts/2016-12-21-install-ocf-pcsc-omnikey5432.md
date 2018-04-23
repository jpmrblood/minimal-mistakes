---
title: Install libOCFPCSC.so, pcscd and Omnikey 5432 driver
tags:
  - omnikey
  - ocf
  - pcsc
  - java
categories:
  - linux
  - driver
  - tips
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2016/12/smartcard.png
  overlay_image: /assets/2016/12/smartcard.png
excerpt: For those who do smart cards, we can use PCSCLite library. With Omnikey 5321 as reader, here's how we do it.
---

Installing necessary driver for Omnikey and install OCFPCSC driver for it.

# Driver Part

## Install PCSC and tools

```console
$ sudo apt install libpcsclite-dev pcscd pcsc-tools
```

## Install Omnikey Driver

Go to HID Global and download: [OMNIKEY 512X, 532X, 1021, 3X21, 6121 PCSC FOR LINUX X86_64](https://www.hidglobal.com/drivers?field_driver_brand_tid_selective=24&field_driver_product_reference_nid_selective=All&field_driver_operating_systems_tid_selective=All)

Actually, use Google and search for *ifdokrfid_lnx_x64-2.10.0.1* version. That is the most stable one in my years of experience. Last time I tested it, the new ones was not that relible. May be have change.

```console
$ tar xvfz ifdokrfid_lnx_x64-2.10.0.1.tar.gz && cd ifdokrfid_lnx_x64-2.10.0.1
$ sudo ./install -d /usr/lib/pcsc/drivers
```

And PCSCd should detect the reader. If not, go restart PCSCd

```console
$ sudo systemctl restart pcscd
```

Or, to debug PCSCd

```console
$ sudo systemctl stop pcscd
$ sudo pcscd -afd
```
Press CTRL+C to terminate it.

To check card:

```console
$ pcsc_scan
PC/SC device scanner
V 1.4.25 (c) 2001-2011, Ludovic Rousseau <ludovic.rousseau@free.fr>
Compiled with PC/SC lite version: 1.8.14
Using reader plug'n play mechanism
Scanning present readers...
0: OMNIKEY CardMan 5321 00 00

Wed Dec 21 09:28:44 2016
Reader 0: OMNIKEY CardMan 5321 00 00
  Card state: Card removed,
```

# Install Java SDK

```console
$ sudo apt-get install openjdk-8-jdk
```

# Install OCFPCSC

Download OCF library from [OpenSCDP site](http://www.openscdp.org/ocf/download.html).

```console
$ wget http://www.openscdp.org/ocf/ocf-1.3.1916.zip
$ unzip ocf-1.3.1916.zip
$ cd ocf/jni/ocfpcsc
$ make JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
$ sudo cp libOCFPCSC1.so /usr/lib/libOCFPCSC1.so
```


Done. Now java app can access card.
