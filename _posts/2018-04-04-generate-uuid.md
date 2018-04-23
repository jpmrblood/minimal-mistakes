---
title: Generating UUID
tags:
  - uuid
  - python
  - kernel
  - sh
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Various ways of generating UUID
---

There are ways of creating UUID.


# From kernel

Directly from kernel

```
UUID=$(cat /proc/sys/kernel/random/uuid)
```


# From Python

Creating version 4 UUID. (Change 4 to 1 if you want version 1)

```
UUID=$(python  -c 'import uuid; print uuid.uuid4()')
```

# From Random numbers

From random numbers.

```
UUID=$(od -x /dev/urandom | head -1 | awk '{OFS="-"; print $2$3,$4,$5,$6,$7$8$9}')
```
