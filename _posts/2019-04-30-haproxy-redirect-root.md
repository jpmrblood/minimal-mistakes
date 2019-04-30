---
title: HAProxy redirect root URL
tags:
  - haproxy
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: How to redirect root URL to another URL
---
How to redirect root URL to another URL

```ini
## Redirect root to somewhere URL
    acl is_root path -i /
    redirect code 301 location /real/app/path if is_root
```