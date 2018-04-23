---
title: Run GC From Commandline
tags:
  - java
  - tomcat
  - gc
categories:
  - java
  - tips
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2017/09/java2.png
  overlay_image: /assets/2017/09/java2.png
excerpt:
---
Run this on the server:
```
$ sudo -u tomcat7 jcmd `cat /var/run/tomcat7.pid` GC.run
```
This is since JDK7. Run jcmd as the same user as the user that runs the Java apps.
