---
title: myslqdump compatible with PostgreSQL
tags:
  - mysql
  - mysqldump
  - postgresql
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Dumping Data To Be Compatible With PostgreSQL
---

This is how we do it, we disable extended insert.

```bash
mysqldump -nt --compatible=ansi,postgresql --complete-insert=TRUE --extended-insert=FALSE --compact --default-character-set=UTF8 -u $DB_USER -p$DB_PASS $DB_NAME $TABLE
```