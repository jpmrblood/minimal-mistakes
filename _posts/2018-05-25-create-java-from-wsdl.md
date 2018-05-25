---
title: Create Java From WSDL
tags:
  - wsdl
  - java
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: How to create a java package from WSDL file.
---
JAX WS client from wsimport, a native tool from Oracle Java.

```bash
$JDK_PATH/bin/wsimport -keep -verbose -p our.own.package $WSDL_FILE_OR_URL
```
