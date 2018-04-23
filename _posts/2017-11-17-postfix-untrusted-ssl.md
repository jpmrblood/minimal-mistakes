---
title: Postfix untrusted SSL
tags:
  - postfix
  - tls
categories:
  - tips
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/admin-talk-300x160.jpg
  overlay_image: /assets/admin-talk-300x160.jpg
excerpt: Warning about untrusted TLS connection when Postfix tries to connect to a server via secure channel.
---
If got this error when sending email to GMail/Yahoo!/etc via secure channel:

```
Untrusted TLS connection established to gmail-smtp-in.l.google.com[74.125.24.26]:25: TLSv1.2 with cipher ECDHE-RSA-AES128-GCM-SHA256 (128/128 bits)
```

Add this line to `/etc/postfix/main.cf`

```
smtp_tls_CApath = /etc/ssl/certs
smtpd_tls_CApath = /etc/ssl/certs
```

and restart Postfix.
