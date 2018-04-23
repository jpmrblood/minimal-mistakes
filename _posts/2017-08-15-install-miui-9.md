---
title: Installing MIUI 9 on Unlocked Xiaomi Mi 6
tags:
  - Android
categories:
  - linux
  - android
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2017/02/android-recharged.png
  overlay_image: /assets/2017/02/android-recharged.png
excerpt: Install MIUI 9, TWRP, and Magisk.
---
# Install MIUI 9
Extract MIUI 9 fastboot package.
```
$ tar xvfz sagit_global_images_7.8.10_20170810.0000.00_7.1_global_8039c40e70.tgz
$ cd sagit_global_images_7.8.10_20170810.0000.00_7.1_global
```
Install without wiping storage. The drawback using this script is that the theme is not gonna get installed.
It's alright. Dozen of people already extract the three MIUI 9 theme MTZs.
```
$ sudo bash flash_all_except_storage.sh
[sudo] password for jp:
product: sagit
erasing 'boot'...
OKAY [  0.007s]
finished. total time: 0.007s
target reported max download size of 536870912 bytes
sending 'crclist' (0 KB)...
OKAY [  0.001s]
writing 'crclist'...
OKAY [  0.002s]
finished. total time: 0.003s
target reported max download size of 536870912 bytes
sending 'sparsecrclist' (0 KB)...
OKAY [  0.000s]
writing 'sparsecrclist'...
OKAY [  0.000s]
finished. total time: 0.001s
target reported max download size of 536870912 bytes
sending 'xbl' (3970 KB)...
OKAY [  0.128s]
writing 'xbl'...
OKAY [  0.104s]
finished. total time: 0.232s
target reported max download size of 536870912 bytes
sending 'xblbak' (3970 KB)...
OKAY [  0.126s]
writing 'xblbak'...
OKAY [  0.135s]
finished. total time: 0.261s
target reported max download size of 536870912 bytes
sending 'abl' (108 KB)...
OKAY [  0.004s]
writing 'abl'...
OKAY [  0.003s]
finished. total time: 0.007s
target reported max download size of 536870912 bytes
sending 'ablbak' (108 KB)...
OKAY [  0.004s]
writing 'ablbak'...
OKAY [  0.005s]
finished. total time: 0.008s
target reported max download size of 536870912 bytes
sending 'tz' (1892 KB)...
OKAY [  0.061s]
writing 'tz'...
OKAY [  0.050s]
finished. total time: 0.111s
target reported max download size of 536870912 bytes
sending 'tzbak' (1892 KB)...
OKAY [  0.060s]
writing 'tzbak'...
OKAY [  0.069s]
finished. total time: 0.129s
target reported max download size of 536870912 bytes
sending 'hyp' (248 KB)...
OKAY [  0.009s]
writing 'hyp'...
OKAY [  0.007s]
finished. total time: 0.016s
target reported max download size of 536870912 bytes
sending 'hypbak' (248 KB)...
OKAY [  0.009s]
writing 'hypbak'...
OKAY [  0.007s]
finished. total time: 0.016s
target reported max download size of 536870912 bytes
sending 'rpm' (228 KB)...
OKAY [  0.008s]
writing 'rpm'...
OKAY [  0.007s]
finished. total time: 0.015s
target reported max download size of 536870912 bytes
sending 'rpmbak' (228 KB)...
OKAY [  0.008s]
writing 'rpmbak'...
OKAY [  0.007s]
finished. total time: 0.015s
target reported max download size of 536870912 bytes
sending 'pmic' (49 KB)...
OKAY [  0.002s]
writing 'pmic'...
OKAY [  0.002s]
finished. total time: 0.004s
target reported max download size of 536870912 bytes
sending 'pmicbak' (49 KB)...
OKAY [  0.002s]
writing 'pmicbak'...
OKAY [  0.002s]
finished. total time: 0.005s
target reported max download size of 536870912 bytes
sending 'devcfg' (56 KB)...
OKAY [  0.002s]
writing 'devcfg'...
OKAY [  0.002s]
finished. total time: 0.004s
target reported max download size of 536870912 bytes
sending 'storsec' (48 KB)...
OKAY [  0.002s]
writing 'storsec'...
OKAY [  0.002s]
finished. total time: 0.004s
target reported max download size of 536870912 bytes
sending 'bluetooth' (380 KB)...
OKAY [  0.013s]
writing 'bluetooth'...
OKAY [  0.011s]
finished. total time: 0.024s
target reported max download size of 536870912 bytes
sending 'cmnlib' (212 KB)...
OKAY [  0.007s]
writing 'cmnlib'...
OKAY [  0.008s]
finished. total time: 0.015s
target reported max download size of 536870912 bytes
sending 'cmnlibbak' (212 KB)...
OKAY [  0.008s]
writing 'cmnlibbak'...
OKAY [  0.008s]
finished. total time: 0.016s
target reported max download size of 536870912 bytes
sending 'cmnlib64' (275 KB)...
OKAY [  0.009s]
writing 'cmnlib64'...
OKAY [  0.010s]
finished. total time: 0.019s
target reported max download size of 536870912 bytes
sending 'cmnlib64bak' (275 KB)...
OKAY [  0.010s]
writing 'cmnlib64bak'...
OKAY [  0.008s]
finished. total time: 0.018s
target reported max download size of 536870912 bytes
sending 'modem' (110524 KB)...
OKAY [  3.545s]
writing 'modem'...
OKAY [  4.501s]
finished. total time: 8.046s
target reported max download size of 536870912 bytes
sending 'dsp' (16384 KB)...
OKAY [  0.518s]
writing 'dsp'...
OKAY [  0.450s]
finished. total time: 0.968s
target reported max download size of 536870912 bytes
sending 'keymaster' (369 KB)...
OKAY [  0.013s]
writing 'keymaster'...
OKAY [  0.011s]
finished. total time: 0.023s
target reported max download size of 536870912 bytes
sending 'keymasterbak' (369 KB)...
OKAY [  0.013s]
writing 'keymasterbak'...
OKAY [  0.013s]
finished. total time: 0.026s
target reported max download size of 536870912 bytes
sending 'logo' (14132 KB)...
OKAY [  0.446s]
writing 'logo'...
OKAY [  0.534s]
finished. total time: 0.980s
target reported max download size of 536870912 bytes
sending 'splash' (167 KB)...
OKAY [  0.006s]
writing 'splash'...
OKAY [  0.024s]
finished. total time: 0.030s
target reported max download size of 536870912 bytes
sending 'misc' (8 KB)...
OKAY [  0.001s]
writing 'misc'...
OKAY [  0.001s]
finished. total time: 0.002s
target reported max download size of 536870912 bytes
erasing 'system'...
OKAY [  0.541s]
sending sparse 'system' 1/7 (515528 KB)...
OKAY [ 23.088s]
writing 'system' 1/7...
OKAY [ 21.534s]
sending sparse 'system' 2/7 (509068 KB)...
OKAY [ 20.232s]
writing 'system' 2/7...
OKAY [ 22.077s]
sending sparse 'system' 3/7 (524282 KB)...
OKAY [ 21.680s]
writing 'system' 3/7...
OKAY [ 21.243s]
sending sparse 'system' 4/7 (518394 KB)...
OKAY [ 21.380s]
writing 'system' 4/7...
OKAY [ 19.992s]
sending sparse 'system' 5/7 (524202 KB)...
OKAY [ 21.734s]
writing 'system' 5/7...
OKAY [ 23.267s]
sending sparse 'system' 6/7 (472247 KB)...
OKAY [ 18.714s]
writing 'system' 6/7...
OKAY [ 20.218s]
sending sparse 'system' 7/7 (81808 KB)...
OKAY [  3.096s]
writing 'system' 7/7...
OKAY [  4.964s]
finished. total time: 263.760s
target reported max download size of 536870912 bytes
erasing 'cache'...
OKAY [  0.008s]
sending 'cache' (6200 KB)...
OKAY [  0.196s]
writing 'cache'...
OKAY [  0.351s]
finished. total time: 0.555s
target reported max download size of 536870912 bytes
sending 'recovery' (22169 KB)...
OKAY [  0.713s]
writing 'recovery'...
OKAY [  0.579s]
finished. total time: 1.292s
erasing 'sec'...
OKAY [  0.000s]
finished. total time: 0.000s
target reported max download size of 536870912 bytes
sending 'cust' (341855 KB)...
OKAY [ 10.859s]
writing 'cust'...
OKAY [ 21.771s]
finished. total time: 32.630s
target reported max download size of 536870912 bytes
sending 'boot' (20085 KB)...
OKAY [  0.631s]
writing 'boot'...
OKAY [  0.682s]
finished. total time: 1.313s
rebooting...

finished. total time: 0.050s
```

# Install TWRP

Get into fastboot:

```
$ adb reboot bootloader
$ sudo fastboot flash recovery twrp-3.1.1-1-sagit.img
$ sudo fastboot boot recovery twrp-3.1.1-1-sagit.img
```

The last line needed to boot to TWRP because MIUI always override the recovery image everytime it boots.

Rename the script to disable:

```
# adb shell mount /system
# adb shell mv /system/bin/install-recovery.sh /system/bin/install-recovery.sh.bak
```

# Install Magisk-v13.5 beta
The beta version is the latest version as I wrote this and it passes Google's Safety Net check.

```
$ adb push Magisk-v13.5\(1350\).zip /sdcard
```

Install from TWRP and we're done.
