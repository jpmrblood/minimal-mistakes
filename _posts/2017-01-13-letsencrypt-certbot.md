---
title: Let's Encrypt in Debian
tags:
  - letsencrypt
  - ssl
  - ocsp
  - site
  - tips
  - nginx
categories:
  - linux
  - nginx
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2017/01/http-cors.png
  overlay_image: /assets/2017/01/http-cors.png
excerpt: How to get Let's Encrypt SSL in Debian
---
# Getting certbot
## Debian Wheezy

```
wget -q https://dl.eff.org/certbot-auto -O-  | sudo tee /usr/local/bin/certbot-auto
sudo chmod +x /usr/local/bin/certbot-auto
```

So

```
export CERTBOT_CMD=/usr/local/bin/certbot-auto
```

## Debian Jessie

```
echo "deb http://ftp.debian.org/debian jessie-backports main" | sudo tee /etc/apt/sources.list.d/debian-backports.list
sudo apt update
sudo apt-get install certbot -t jessie-backports
```
So

```
export CERTBOT_CMD=/usr/bin/certbot
```

# Prerequisites

## Enable domains in public DNS first.

You know what to do here.

## Ensure .well-known is accessible via plain HTTP.

```
server {
        listen   80;
        listen  [::]:80 ipv6only=on;
        server_name  example.com www.example.com;
        server_name_in_redirect on;
        port_in_redirect on;

        access_log  /var/log/nginx/access.log;
        error_log  /var/log/nginx/error.log;

        # For ACME Let's Encrypt challenge
        location /.well-known {
                alias /var/www/html/.well-known; # have this as the webroot
        }

        location / {
                return 301 https://$server_name$request_uri;
        }

}
```

# Install

```
$CERTBOT_CMD certonly --webroot -w /var/www/html -d example.com -d www.example.com
```

# Install in Web Server

## Certificate

```
ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
```

## Private Key

```
ssl_certificate_key /etc/letsencrypt/live/example/privkey.pem;
```

## OCSP Stapling

```
ssl_trusted_certificate /etc/letsencrypt/live/example/chain.pem;
```

## Full Example

```
ssl  on;

ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
ssl_certificate_key /etc/letsencrypt/live/example/privkey.pem;

ssl_protocols       TLSv1 TLSv1.1 TLSv1.2;
ssl_ciphers         "EECDH+ECDSA+AESGCM EECDH+aRSA+AESGCM EECDH+ECDSA+SHA384 EECDH+ECDSA+SHA256 EECDH+aRSA+SHA384 EECDH+aRSA+SHA256 EECDH+aRSA+RC4 EECDH EDH+aRSA RC4 !aNULL !eNULL !LOW !3DES !MD5 !EXP !PSK !SRP !DSS";
ssl_prefer_server_ciphers on;
ssl_session_cache   shared:SSL:20m;
ssl_session_timeout 60m;

ssl_dhparam /etc/nginx/ssl/dhparam.pem;

ssl_stapling on;
ssl_stapling_verify on;
ssl_trusted_certificate /etc/letsencrypt/live/example/chain.pem;
resolver 8.8.8.8;

add_header Strict-Transport-Security "max-age=31536000" always;
```

# Renewal

## Debian Jessie

It's automatic.

## Debian Wheezy

Test dry-run.

```
$CERTBOT_CMD renew --dry-run
```

If runs well, add to root's CRON job.

```
0 */6 * * * /usr/local/bin/certbot-auto renew --quiet --no-self-upgrade && /etc/init.d/nginx reload > /dev/null 2>&1
```
