---
title: CAS with LDAP Authentication
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
excerpt: CAS uses LDAP for real authentication!
---

# Conventions

```bash
export CAS_SRC_DIR=`pwd` # somewhere
```

Yes, I assume we are on root directory of our CAS Gradle overlay.

# Configure CAS

## CAS Project

Add dependency at `$CAS_SRC_DIR/cas/build.gradle`:

```gradle
compile "org.apereo.cas:cas-server-support-ldap:${project.'cas.version'}"
```

## Configuration

Add to `$CAS_SRC_DIR/etc/cas/config/cas.properties`:

```yaml
# Disable casuser
cas.authn.accept.users=

# LDAP authentication
cas.authn.ldap[0].type=ANONYMOUS
cas.authn.ldap[0].ldapUrl=ldaps://ldap.example.org:636
cas.authn.ldap[0].useSsl=true
cas.authn.ldap[0].baseDn=dc=example,dc=org
cas.authn.ldap[0].userFilter=uid={user}
```

It is needed that we access LDAP via SSL/TLS connection. For OpenLDAP, we must specify the port.

# Re-deploy

```bash
./deploy package
./deploy run
```

# References

 - [Installation: LDAP Authentication](https://apereo.github.io/cas/5.2.x/installation/LDAP-Authentication.html)
 - [Configuration Properties: LDAP Authentication](https://apereo.github.io/cas/5.2.x/installation/Configuration-Properties.html#ldap-authentication-1)
