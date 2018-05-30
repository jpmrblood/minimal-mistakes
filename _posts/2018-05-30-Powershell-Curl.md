---
title: Powershell Curl
tags:
  - powershell
  - curl
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: CUrl in Powershell.
---

Powershell making `curl` as an alias to `Invoke-Webrequest`. 

```sh
Invoke-WebRequest http://yourURLhere -Headers @{"accept"="application/json"}
```

[Invoke-WebRequest](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest?view=powershell-5.1)

[stackoverflow](https://stackoverflow.com/questions/12936150/is-it-possible-to-send-additional-http-headers-to-web-services-via-new-webservic)