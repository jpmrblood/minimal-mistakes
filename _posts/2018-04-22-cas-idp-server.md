---
title: Install CAS IdP server
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

#  Installation

Just to make sure, we are in the project's root directory:
```bash
cd $CAS_SRC_DIR
```

## Compilation
Change Tomcat to Jetty

```bash
sed -i "s/tomcat/jetty/" cas/build.gradle
```

Now compile:
```bash
./build clean build
```


## Setup
Setup basic configuration.

```bash
cat > etc/config/cas.properties << EOF
# server.port = 8443
cas.server.name: https://$DOMAIN_NAME:8443
cas.server.prefix: https://$DOMAIN_NAME:8443/cas

cas.adminPagesSecurity.ip=127\.0\.0\.1

logging.config: file:/etc/cas/config/log4j2.xml
# cas.serviceRegistry.config.location: classpath:/services

# SSL
server.ssl.enabled=true

server.ssl.keyStore=file:/etc/cas/$DOMAIN_NAME.keystore
server.ssl.keyStorePassword=$KEYSTORE_PASS
server.ssl.keyPassword=$KEYSTORE_PASS
EOF

```
> Yeah, I just borrowed the lines from original cas.properties, change the domain name and add keystore for SSL connection.

## Install

Make configuration directory:

```bash
sudo mkdir /etc/cas
sudo chown `whoami`:`whoami` /etc/cas
```

In production, we should create a CAS user login for the job. But for now, just use our own login.


Copy the configurations:

```bash
./build copy
```


# Run the CAS APP.

```bash
./build run
```

Open your browser, the default user is `casuser` and the password is `Mellon`. Remember, we haven't provide any *REAL* identity authentication. This is still for development, not yet production.

![CAS default login](/assets/2018/04/cas_default_login.png)


# TODO

 - Create CAS user login.
 - Create personalized login page.
 - Create systemd unit.
 - Setup authentication provider. Usually, LDAP or DB. But, I see we could make our own RESTful service as an authentication provider. Neat!
 - Create proper configuration. This is not so FHS!
 - Install package instead of messing with source code.
