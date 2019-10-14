---
title: Installing Oracle JDBC to Local Maven Repo
tags:
  - oracle
  - database
  - jdbc
  - maven
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/2018/04/java2.png
  overlay_image: /assets/2018/04/java2.png
excerpt: How to install Oracle JDBC to Maven repo
---

Get `odbc8.jar` from Oracle instant client or any Oracle client installation.

Using a local Maven project, copy and run:

```bash
mvnw install:install-file -Dfile=ojdbc8.jar -DgroupId=com.oracle -DartifactId=ojdbc8 -Dversion=12.2.0.1 -Dpackaging=jar
```

Change ojdbc8.jar location for custom path.

# Maven Entry

```xml
<dependency>
  <groupId>com.oracle</groupId>
  <artifactId>ojdbc8</artifactId>
  <version>12.2.0.1</version>
	<scope>runtime</scope>
</dependency>
```