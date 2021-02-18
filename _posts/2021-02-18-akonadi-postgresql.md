---
title: Use PostgreSQL in Akonadi
tags:
  - kde
  - ubuntu
  - akonadi
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: How to enable akonadi with PostgreSQL as backend.
---
Stop Akonadi server first:

```sh
akonadictl stop
```

Install:

```sh
sudo apt install postgresql-12 akonadi-backend-postgresql
```

Change `postgresql-12` with `postgresql` or whichever exists on your distro.
I'm using latest KDE Neon.

Create a configuration file `$HOME/.config/akonadi/akonadiserverrc`
The content:

```conf
[%General]
Driver=QPSQL

[QPSQL]
Host=/tmp/akonadi-user.RqiEZ0
InitDbPath=/usr/lib/postgresql/12/bin/initdb
Name=akonadi
Options=
ServerPath=/usr/lib/postgresql/12/bin/pg_ctl
StartServer=true
```

Change `InitDbPath` and `ServerPath` if you use different PostgreSQL.

Start Akonadi and check its integrity.

```sh
akonadictl stop
akonadictl fsck
```

Source:
https://prkos.hr/KOrganizer-and-Akonadi-Ubuntu-with-Postgres
