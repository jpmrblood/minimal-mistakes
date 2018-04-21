---
title: PEM to Java Keystore
tags:
  - java
  - jdk
  - pem
  - keystore
  -pkcs12
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  overlay_image: /assets/2018/04/java2.png
excerpt: Installing Oracle Java 10 JDK on Debian Stretch
---


```bash
openssl pkcs12 -export -in ui.ac.id.crt -inkey ui.ac.id.key -out thekeystore -name cas -certfile ui.ac.id.crt
```

# Note

The `keytool` command warns this after creating of a keystore:
> The JKS keystore uses a proprietary format. It is recommended to migrate to PKCS12 which is an industry standard format using "`keytool -importkeystore -srckeystore clientkeystore -destkeystore clientkeystore -deststoretype pkcs12`".

But, hey, every Java thing still only able to load keystore, not PKCS12.

# Reference

[]""
