---
title: Delete Filename Too Long in Windows
tags:
  - windows
  - 2012R2
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: How to delete long filename in Windows
---
Old Windows can't delete files that have more than 260 path name.
So, use robocopy to deal with it.

```sh
mkdir emptyfolder
robocopy emptyfolder folderwithtoolongpathnames /purge
```

Source:
https://helpcenter.gsx.com/hc/en-us/articles/115002767907-How-to-Clean-Folder-Contents-when-a-Filename-or-File-Path-is-to-long