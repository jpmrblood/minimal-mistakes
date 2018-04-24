---
title: CAS Case Study, Wordpress
tags:
  - cas
  - wordpress
  - sso
categories:
  - cas
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/2018/04/java2.png
  overlay_image: /assets/2018/04/java2.png
excerpt: CAS Case Study, Wordpress
---

# Conventions

I install wordpress at `https://example.org:10443/`

# Server Setup

## PHP 7.2

Install from Sury's.

```bash
wget -O- https://packages.sury.org/php/apt.gpg | sudo apt-key add -
echo "deb https://packages.sury.org/php/ stretch main" | sudo tee  /etc/apt/sources.list.d/php-sury.list
sudo apt update
sudo apt install php7.2-fpm php7.2-curl php7.2-gd php7.2-imagick php7.2-json php7.2-mysql php7.2-readline php-redis php7.2-xml php7.2-mbstring php7.2-zip php7.2-mysql php7.2-curl -y
```

## MariaDB/MySQL

Install the server

```bash
sudo apt install mariadb-server
```

Create database for Wordpress:

```bash
sudo mysql --defaults-file=/etc/mysql/debian.cnf

create database wpdb;
grant all privileges on wpdb.* to 'wp'@'%' identified by 'g4ntiB0S5';
flush privileges;
quit
```

## NGINX

```bash
sudo apt install nginx-light
```

At this point I am not ashamed to admit that I'm using VMs on my desktop (VirtualBox).
And, for some reason my browser won't show plain HTTP. That's why my configuration is
HTTPS all the way! I don't like surprises just for case study, so I made the port as
the same as the VirtualBox port forwarding.

The SSL config is `snakeoil-ui`, a `snakeoil` snippet changed to use my own valid SSL
certs. As I said, no surprise!

```nginx
server {
        listen 10443 ssl default_server;
        listen [::]:10443 ssl default_server;
        include snippets/snakeoil-ui.conf;
        root /var/www/html;
        index index.html index.htm index.nginx-debian.html index.php;

        server_name example.org;

        location / {
                try_files $uri $uri/ /index.php$is_args$args;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
        }

        location ~ /\.ht {
                deny all;
        }
}
```

I changed `server_name` from `_` to `example.org`, a valid FQDN. WP Cassify uses `$server_name`
as its identifier to CAS. It made CAS failed redirected back into our WP site.

```bash
sudo systemctl restart nginx
```

## Wordpress

Get WP-CLI

```bash
sudo wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar -O /usr/local/bin/wp
sudo chmod +x /usr/local/bin/wp
```

We're gonna install in default Debian path.

```bash
sudo chown 33:33 /var/www/html
sudo -u www-data wp core download  --path=/var/www/html
```

Open browser to setup as usual.

## Wordpress Plugin

{% include figure image_path="/assets/2018/04/wp-cassify.png" alt="Search and install WP Cassify." caption="Search and install WP Cassify." %}


# Configure SSO Service

## CAS Service

Go to `https://example.org:9443/cas-management/`

`Add New Service` in the menu.

### Basic

Service Type | CAS Client
Service URL | `^https://example.org:10443/.*`
Service Name | Wordpress Cassify
Description | Wordpress Cassified.

And then Save Changes.

## WP Cassify

After installing WP Cassify, go to `Options` &rarr; `WP Cassify`. Select:

|CAS Server base url:| https://example.org:8443/cas|
|Create user if not exist:| (x)|

Map a user or group to Administrator role.

| Push defaults roles to connected user | Administrator |
| | `(CAS{cas_user_id} -EQ "casuser")` |

Save them all.
