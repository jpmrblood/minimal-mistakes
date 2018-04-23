---
title: Netdata Postfix Alarm
tags:
  - netdata
  - linux
  - postfix
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Netdata postfix local alarm
---

`/etc/netdata/health.d/postfix.conf:`

```
template: postfix_local_queue
      on: postfix.qemails
   every: 10s
    calc: $emails
    warn: $this > 20
    crit: $this > 100
      to: sysadmin
    info: number of emails in the postfix queue
```

Source:

<https://github.com/firehol/netdata/issues/2567>
