---
title: Search and Replace Trailing Space in Libreoffice
tags:
  - libreoffice
  - search
  - replace
  - function
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2018/02/libredark.png
  overlay_image: /assets/2018/02/libredark.png
excerpt: Replace trailing space with `^[ ]+|[ ]+$`
---
Edit > Find & Replace

    Search for: ^[ ]+|[ ]+$
    Replace with:
    Options: Regular expressions: ON
    Click "Replace All".

In English, that pattern matches:

    Beginning of text
    A space, zero or more times
    (Any character, zero or more times)
    A space, zero or more times
    End of text

The replacement represents the text that matched the part in parentheses, or everything except the spaces at the end.

[Source](https://forum.openoffice.org/en/forum/viewtopic.php?f=9&t=15879&start=0)
