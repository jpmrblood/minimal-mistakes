---
title: ViM on sources.list
tags:
  - vim
  - sources.list
  - regex
categories:
  - tips
---

Changing all default repo URLs to KAMBING.ui.ac.id:

```console
:%s/\/\/.*\//\/\/kambing.ui.ac.id\/ubuntu/g
```
