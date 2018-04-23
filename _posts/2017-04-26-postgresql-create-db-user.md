---
title: PostgreSQL Create User and Database
tags:
  - postgresql
  - debian
categories:
  - database
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/2018/04/database.png
  overlay_image: /assets/2018/04/database.png
---
How to create user and database in PostgreSQL.

```
$ sudo -u postgres createuser -D -A -P myUser
Enter password for new role:
Enter it again:

$ sudo -u postgres createdb -O myUser myDB
```
