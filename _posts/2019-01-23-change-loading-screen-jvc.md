---
title: Change Loading Screen 
tags:
  - car
  - firmware
categories:
  - ertiga
header:
  teaser: /assets/2019/01/image1.jpg
  overlay_image: /assets/2019/01/image1.jpg
excerpt: New Screen Loading on JVC KW-M540BT
---
WARNING2: I'm not responsible for any use of this info. The responsibility is yours.

All New Ertiga 2018 GX uses JVC KW-M540BT. I've flashed the OEM with updated firmware. Well, I need to change the loading screen from default JVC logo to something else.


# USB Drive

There are two files that should go into USB Drive:

* The image
* `OpeningCustomize.txt` text file.

Format USB to FAT32 first before putting the files.

## The Logo

We need to get the logo.

* Create image 914x480 and compress it to 800x480.
* Save the image as 16-bit BMP image.

I named the image `image1.bmp` because of creativity. :P

## The  `OpeningCustomize.txt`

Its content:
```
Opening Customize
[FILE]image1.bmp
[VERSION]9876
~END
```

# Get It

Put the USB drive at the USB drive on the car. Go to `A/V Off` screen.

On that screen, touch twice on the upper left, touch twice on the bottom left (above the app button), touch the upper left again once, and last touch the bottom left once.

The menu would be out and select the first button.

Done.

Source:
* [How to change Kenwood load screen](https://carboncarsystems.com.au/how-to-change-jvc-kenwood-load-screen/)

<iframe width="560" height="315" src="https://www.youtube.com/embed/zzMevvZEKjs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

