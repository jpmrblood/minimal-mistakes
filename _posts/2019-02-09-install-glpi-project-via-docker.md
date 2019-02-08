---
title: Install GLPI Project via Docker 
tags:
  - glpi
  - docker
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Installing GLPI Project via Docker 
---
First, let's have a password
```
export MARIADB_PWD=`pwgen 16 1` 
```

Remember it:
```
echo $MARIADB_PWD
```

Set HTML directory:
```
docker create --name glpi-data --volume /var/www/html/glpi:/var/www/html/glpi busybox /bin/true
```

I'll be using MariaDB to navigate away from Oracle.
Install MariaDB
```
docker run -d --name mysql-glpi -eMARIADB_ROOT_PASSWORD=$MARIADB_PWD mariadb/server:10.3
```

Install GLPI Project:
```
docker run --name glpi --hostname glpi --link mysql-glpi:mariadb --volumes-from glpi-data -p 80:80 -d diouxx/glpi
```

# Installation Wizard

Installation Wizard are based on docs:
[https://glpi-install.readthedocs.io/en/latest/install/wizard.html](https://glpi-install.readthedocs.io/en/latest/install/wizard.html)

Everything is just click next. But, the highlighted one is at the DB:

```
SQL Server: MariaDB
SQL User: root
SQL Password: $MARIADB_PWD
```

done.