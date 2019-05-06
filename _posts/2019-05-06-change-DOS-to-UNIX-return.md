---
title: Change DOS to UNIX Line Ending
tags:
  - bash
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: How to change line ending format
---
How to change line ending format

```sh
for file in *.cpp
do 
    vi +':w ++ff=unix' +':q' "$file"
done
```

Source:
https://stackoverflow.com/a/95650