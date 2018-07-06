---
title: dnscrypt-proxy on Android
tags:
  - dnscrypt
  - client
  - android
categories:
  - tips
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2016/12/dns-crypt.png
  overlay_image: /assets/2016/12/dns-crypt.png
---
My 4G provider's DNS throttling my 4G experience.

# Install DNSCrypt 

Flash from [the latest ZIP provided by palmuse](https://github.com/jedisct1/dnscrypt-proxy/issues/41#issuecomment-402154764)

# Run (Manually) from Rooted Terminal

```sh
dnscrypt-proxy --config /etc/dnscrypt-proxy/dnscrypt-proxy.toml
```

Wait until it finished starting.

# Add a local VPN to use DNSCrypt

Install [dnschanger](https://play.google.com/store/apps/details?id=com.frostnerd.dnschanger)
Use Advanced Settings from dnschanger to enable localhost.
Add new DNS profile with 127.0.0.1 as the DNS 1 and let DNS 2 empty. 

# Voila!

Now IPLeak shows my real IP.

![IP Leak shows my real IP](/assets/2018/07/ipleaks-dnscrypt.png)

# Source 

- [Running dnscrypt-proxy on Android](https://github.com/jedisct1/dnscrypt-proxy/issues/41) 