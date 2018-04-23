---
title: ViM on sources.list
tags:
  - vim
  - sources.list
  - regex
categories:
  - tips
header:
  teaser: /assets/2016/12/vim.png
  overlay_image: /assets/2016/12/vim.png
---

Changing all default repo URLs to KAMBING.ui.ac.id:

```console
:%s/\/\/.*\//\/\/kambing.ui.ac.id\/ubuntu/g
```
