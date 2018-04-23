---
title: npm Update Error
tags:
  - npm
  - linux
  - nodejs
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: npm Update Error
---

## Problem

```bash
$ sudo npm i -g npm to update
npm ERR! code 1
npm ERR! Command failed: /usr/bin/git clone -q git://github.com/jonschlinkert/resolve-file.git /home/jp/.npm/_cacache/tmp/git-clone-6677f267
npm ERR! /home/jp/.npm/_cacache/tmp/git-clone-6677f267/.git: Permission denied
npm ERR!

npm ERR! A complete log of this run can be found in:
npm ERR!     /home/jp/.npm/_logs/2018-04-11T09_43_12_553Z-debug.log
```

## Solution

```bash
$ wget -O- https://www.npmjs.com/install.sh | sudo bash
```
