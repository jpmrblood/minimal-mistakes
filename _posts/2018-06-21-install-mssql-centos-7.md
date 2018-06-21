---
title: Install MSSQL to CentOS 7
tags:
  - mssql
  - centos
  - database
categories:
  - centos
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Install a MS SQL Express to CentOS 7.
---
Just to make sure:

```bash
sudo yum update
```

Get the YUM package:

```bash
 sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo
 ```

Install MS SQL:

```bash
sudo yum install -y mssql-server
```

Setup server:

```bash
sudo /opt/mssql/bin/mssql-conf setup
```

Open network firewall for 1433 (default port for MSSQL) so that it could be accessed from other machine.

```bash
sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
sudo firewall-cmd --reload
```

Done.

# SOURCE

* [Quickstart: Install SQL Server and create a database on Red Hat](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-red-hat?view=sql-server-linux-2017)