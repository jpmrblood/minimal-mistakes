---
title: Image to PDF
tags:
  - pdf
  - image
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Adding Images to single PDF
---

Adding images to pdf:

```sh

convert 1.jpg 2.jpg output.pdf

```

Compress:

```sh
gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -dNOPAUSE -dQUIET -dBATCH -sOutputFile=input.pdf output.pdf
```

Another way to compress:

```sh
ps2pdf input.pdf output.pdf
```