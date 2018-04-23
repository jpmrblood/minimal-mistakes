---
title: Wordpress Salts
tags:
  - site
  - wordpress
categories:
  - wordpress
  - tips
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2017/01/http-cors.png
  overlay_image: /assets/2017/01/http-cors.png
excerpt: How to get generated salts
---

To get wordpress salts:
```console
$ curl https://api.wordpress.org/secret-key/1.1/salt/
```
