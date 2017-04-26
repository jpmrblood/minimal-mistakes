---
title: PostgreSQL Create User and Database
tags:
  - postgresql
  - debian
categories:
  - database
---
How to create user and database in PostgreSQL.

```
$ sudo -u postgres createuser -D -A -P myUser
Enter password for new role:
Enter it again:

$ sudo -u postgres createdb -O myUser myDB
```
