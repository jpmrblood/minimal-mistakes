---
title: GIT Ignore SSL Certs
tags:
  - git
  - ssl
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: How to ignore SSL certs.
---
Sometimes you can't clone because of self-signed certificate:

```bash
Cloning into 'a-project'...
fatal: unable to access 'https://example.local/a-project/': schannel: next InitializeSecurityContext failed: SEC_E_UNTRUSTED_ROOT (0x80090325) - The certificate chain was issued by an authority that is not trusted.
```

No time to download chain certs, just ignore:

```bash
git config --global http.sslVerify false
```

Source:

[https://discourse.gitea.io/t/error-when-cloning-via-https/147/2](https://discourse.gitea.io/t/error-when-cloning-via-https/147/2)
