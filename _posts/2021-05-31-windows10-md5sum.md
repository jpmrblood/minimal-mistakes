---
title: Windows 10 MD5sum
tags:
  - windows
  - md5sum
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: How to check md5sum.
---

Check on a file:

```powershell
CertUtil -hashfile <path to file> MD5
```

Source:
https://onthefencedevelopment.com/2017/08/15/windows-10-builtin-md5-checksum-calculator/
