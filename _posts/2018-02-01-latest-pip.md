---
title: Install Latest PIP
tags:
  - python
  - debian
  - pip
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Install latest PIP.
---
There are ways to install latest PIP in Python3.

# Bootstrap

Install in user directory.

```bash
wget -O- https://bootstrap.pypa.io/get-pip.py | python3
```

# A Little Bit Debian

Install in system-wide.

```bash
sudo apt install python3-pip
sudo pip3 install --upgrade setuptools
```
