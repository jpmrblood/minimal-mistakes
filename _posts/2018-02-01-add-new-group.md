---
title: Add New Group to Current User
tags:
  - shell
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Add new group.
---
```bash
sudo gpasswd -a `whoami` agroup
newgrp agroup
```

Command `newgrp` just so that I don't have to restart my current shell session.
