---
title: Install CAS IdP server
tags:
  - java
  - cas
  - idp
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  overlay_image: /assets/2018/04/java2.png
excerpt: Install CAS server.
---

# Conventions

```bash
export KEYSTORE_PASS=`pwgen 32`
export DOMAIN="example.org"
```

# Requirements

```bash
sudo apt install -y openjdk-8-jdk-headless unzip
```

# Content

```bash
wget --content-disposition https://github.com/apereo/cas-gradle-overlay-template/archive/master.zip
unzip cas-gradle-overlay-template-master.zip && cd cas-gradle-overlay-template-master
```

For convention:
```bash
export CAS_SRC_DIR=`pwd`
```

# Prepare Keystore

There are two common ways we can provide the certificate; by using pre-made SSL
or by making a self-signed. Copy that certificate to project's config dir (`$CAS_SRC_DIR/etc/config/`)

## Pre-made Signed PEM

I assume that your organization have valid PEM. A Let's Encrypt or signed by commercial PKI.

Conventions:

```bash
export KEYSTORE_PASS="changeit"
export DOMAIN_NAME="example.org"
export PEM_DIR=$HOME
```

Convert PEM to keystore/

```bash
openssl pkcs12 -export -in $PEM_DIR/$DOMAIN_NAME.crt -inkey $PEM_DIR/$DOMAIN_NAME.key -out $PEM_DIR/$DOMAIN_NAME.p12 -name $DOMAIN_NAME -passout pass:$KEYSTORE_PASS

keytool -importkeystore -deststorepass $KEYSTORE_PASS -destkeypass $KEYSTORE_PASS -destkeystore $CAS_SRC_DIR/etc/cas/$DOMAIN_NAME.keystore -srckeystore $PEM_DIR/$DOMAIN_NAME.p12 -srcstoretype PKCS12 -srcstorepass $KEYSTORE_PASS -alias $DOMAIN_NAME
```

## Self-signed

```bash
keytool -genkey -keystore $CAS_SRC_DIR/$DOMAIN_NAME.keystore -alias $DOMAIN_NAME -keyalg RSA -keysize 4096 -validity 720
```

#  Compilation

Change Tomcat to Jetty

```bash
sed -i "s/tomcat/jetty/" cas/build.gradle
```
