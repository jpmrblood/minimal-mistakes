---
title: CAS Service Registry with PostgreSQL Backend
tags:
  - java
  - cas
  - idp
categories:
  - cas
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/2018/04/java2.png
  overlay_image: /assets/2018/04/java2.png
excerpt: Building CAS Service Registry with PostgreSQL JDBC backend
---

# Conventions

Yes, I'm using Debian Stretch.

At this point I'm too lazy to write more details.

# Setup PostgreSQL

```bash
echo "deb http://kambing.ui.ac.id/postgresql/repos/apt/ stretch-pgdg main" | sudo tee /etc/apt/sources.list.d/postgresql.list
wget --quiet -O - http://kambing.ui.ac.id/postgresql/repos/apt/ACCC4CF8.asc | sudo apt-key add -
sudo apt update
sudo apt install postgresql-10
```

Create new user and database.

```bash
sudo -u postgres createuser -D -A -P casig
sudo -u postgres createdb -O casig casigdb
```

Add access for all remote clients.

```bash
sudo tee -a /etc/postgresql/10/main/pg_hba.conf << EOF
host    all             all              0.0.0.0/0                       md5
host    all             all              ::/0                            md5
EOF
```

Restart PostgreSQL server.

```bash
sudo /etc/init.d/postgresql restart
```

# CAS Service Registry

Add to CAS' gradle build dependencies:

```gradle
compile "org.apereo.cas:cas-server-support-jdbc-drivers:${project.'cas.version'}"
compile "org.apereo.cas:cas-server-support-jpa-service-registry:${project.'cas.version'}"
```

Add to `etc/cas/config/cas.properties`:

```yaml
cas.serviceRegistry.jpa.url=jdbc:postgresql://192.0.2.9/casigdb
cas.serviceRegistry.jpa.user=casig
cas.serviceRegistry.jpa.password=cimeiwoh7pee4eeg0kae6Jaeyee3Oof7
cas.serviceRegistry.jpa.ddlAuto=update
cas.serviceRegistry.jpa.driverClass=org.postgresql.Driver
cas.serviceRegistry.jpa.dialect=org.hibernate.dialect.PostgreSQL95Dialect
```

Don't forget the dialect or later we would not have DDL.

## Default services

This would install default service for HTTPS/IMAPS. It should be automatically
installed by CAS on the first run. But, hey, may be something goes wrong and we
need to make our own service.

```sql
insert into regexregisteredservice (id, name, serviceid, evaluation_order)
  values (1, 'Generic HTTPS and IMAPS', '^(https?|imaps?|http?)://.*', 0);
```  

## Test

```
casigdb=> \dt
                          List of relations
 Schema |                    Name                    | Type  | Owner
--------+--------------------------------------------+-------+-------
 public | regexregisteredservice                     | table | casig
 public | regexregisteredserviceproperty             | table | casig
 public | registeredservice_contacts                 | table | casig
 public | registeredserviceimpl_props                | table | casig
 public | registeredserviceimplcontact               | table | casig
 public | samlregisteredservice_attributenameformats | table | casig
(6 rows)

```

# References

[JDBC Drivers, PostgreSQL](https://apereo.github.io/cas/5.2.x/installation/JDBC-Drivers.html#postgresql)
[Configuration Properties, Database Service Registry](https://apereo.github.io/cas/5.2.x/installation/Configuration-Properties.html#database-service-registry)
