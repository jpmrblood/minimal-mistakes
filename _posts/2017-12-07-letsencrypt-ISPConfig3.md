---
title: Let's Encrypt in ISPConfig3
tags:
  - letsencrypt
  - ssl
  - ispconfig3
  - site
  - tips
categories:
  - linux
  - apache
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2017/01/http-cors.png
  overlay_image: /assets/2017/01/http-cors.png
excerpt: How to get Let's Encrypt SSL in ISPConfig3
---
It's actually not that difficult. ISPConfig3 already sets the option there. We just need to provide all the necessary tools.

# Getting certbot

Refer to [Let’s Encrypt in Debian](//jpmrblood.github.io/linux/nginx/letsencrypt-certbot/) for Wheezy or manual setup.

For Debian 8 Jessie, enable Backports repo to install `certbot`.

```bash
echo "deb http://ftp.debian.org/debian jessie-backports main" | sudo tee /etc/apt/sources.list.d/debian-backports.list
sudo apt update
sudo apt install certbot -t jessie-backports
```

For Debian 9 Stretch, you just have to install it.

```bash
sudo apt install certbot
```

According [Perfect Guide tutorial](https://www.howtoforge.com/tutorial/perfect-server-debian-8-4-jessie-apache-bind-dovecot-ispconfig-3-1/2/#-install-lets-encrypt), we have to make a directory. I don't know if this is a necessary thing to do. I'm doing it just for the sake of completeness.

```bash
sudo mkdir /opt/certbot
sudo ln -s /usr/bin/certbot /opt/certbot/certbot-auto
```

Done.
