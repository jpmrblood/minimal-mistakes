---
title: Remove First Line Injection
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
excerpt: How remove injection on the first line.
---
The crack injects all of PHP files in the first line with the form:
```
<?php ...../** INJECTED CODE  */ ?> <?php
// NORMAL LINES
...
```
Remove first line that get injected on all PHP files:
```console
find ./ -iname '*.php' -exec  sed -i '1 s/<?php/\n&/2;s/<?php.*\n//' {} \;
```
