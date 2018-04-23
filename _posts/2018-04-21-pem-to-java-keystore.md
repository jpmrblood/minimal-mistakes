---
title: PEM to Java Keystore
tags:
  - java
  - jdk
  - pem
  - keystore
  - pkcs12
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/2018/04/java2.png
  overlay_image: /assets/2018/04/java2.png
excerpt: PEM to Java Keystore
---

Normally, we used PKCS12 PEM for NGINX, Apache2, OpenLDAP, postfix, etc.

BUT NOT JAVA! :P

# Conventions

```bash
export PASS=changeit
export DOMAIN=example.org
```

I'm too lazy, just streamlined it all. :P

# Import

```bash
openssl pkcs12 -export -in $DOMAIN.crt -inkey $DOMAIN.key -out $DOMAIN.p12 -name $DOMAIN -passout pass:$PASS
keytool -importkeystore -deststorepass $PASS -destkeypass $PASS -destkeystore $DOMAIN.keystore -srckeystore $DOMAIN.p12 -srcstoretype PKCS12 -srcstorepass $PASS -alias $DOMAIN
```

# Note

The `keytool` command warns this after creating of a keystore:
> The JKS keystore uses a proprietary format. It is recommended to migrate to PKCS12 which is an industry standard format using "`keytool -importkeystore -srckeystore clientkeystore -destkeystore clientkeystore -deststoretype pkcs12`".

But, hey, every Java thing still only able to load keystore, not PKCS12.

# Reference

[Mengubah Format PEM (Apache/NGINX) ke Keystore JAVA](https://staff.blog.ui.ac.id/jp/2015/10/23/mengubah-format-pem-apachenginx-ke-keystore-java/)
[Chapter 6. Configuring Jetty Connectors: Configuring SSL/TLS](http://www.eclipse.org/jetty/documentation/current/configuring-ssl.html)
