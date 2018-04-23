---
title: Getting LDAP Epoch
tags:
  - ldap
categories:
  - ldap
  - terminal
  - php
  - tips
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/admin-talk-300x160.jpg
  overlay_image: /assets/admin-talk-300x160.jpg
excerpt:
---
Run this on the server:
```
$ echo ' <?php echo strtotime("+185 days")/86400;' | php
```
This is to have date 185 days from today in LDAP format. Useful to set LDAP expiry date.
