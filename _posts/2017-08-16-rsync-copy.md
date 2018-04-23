---
title: RSYNC Copy
tags:
  - shell
categories:
  - shell
  - tips
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: RSYNC copy
---
RSYNC copy all in a folder:
```console
rsync -avz -e "ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null" --progress [DIRECTORY] username@[DESTINATION]:[/*]
```
