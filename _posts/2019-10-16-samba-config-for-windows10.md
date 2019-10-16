---
title: SAMBA config that works on Windows 10
tags:
  - samba
  - windows
  - smb
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: SAMBA config that works on Windows 10
---

SAMBA4 configuration that enable shared document.
However, for newer Windows 10, [Anonymous access must be enabled from Registry](/notes/samba-windows10/).

```ini
# Global parameters
[global]
        client max protocol = SMB3
        client min protocol = SMB2
        dns proxy = No
        log file = /var/log/samba/log.%m
        map to guest = Bad User
        max log size = 1000
        ntlm auth = ntlmv1-permitted
        panic action = /usr/share/samba/panic-action %d
        server min protocol = SMB2
        server role = standalone server
        server string = %h server (Samba, Ubuntu)
        unix extensions = No
        usershare allow guests = Yes
        idmap config * : backend = tdb
        wide links = Yes


[shares]
        create mask = 0664
        directory mask = 0775
        guest ok = Yes
        guest only = Yes
        path = /shares
        read only = No
        valid users = nobody
```