---
title: Stripping Ubuntu Desktop to Ubuntu Server
tags:
  - ubuntu
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: How to remove packages and stripping Ubuntu Desktop
---

Remove all the desktop:

```bash
sudo apt -y remove --purge ubuntu-desktop ubuntu-desktop-minimal gdm3 pulseaudio
sudo apt -y autoremove --purge
```