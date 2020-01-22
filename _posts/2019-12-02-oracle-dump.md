---
title: Oracle Dump
tags:
  - oracle
  - database
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/2018/04/java2.png
  overlay_image: /assets/2018/04/java2.png
excerpt: Setup free font replacement for notorious MS fonts
---

```sh
 expdp \"sys/passwd@localhost/db as sysdba\" schemas=schema1 file=schema1.dmp log=schema1.log
```

May need to create profile first:
```sql
CREATE PROFILE "ABC_PROFILE" LIMIT IDLE_TIME 15;
```