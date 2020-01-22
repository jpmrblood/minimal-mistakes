---
title: Installing Microsoft SQL Server 2017 on Windows 10 with Firewall
tags:
  - mssql
  - windows
  - smb
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Windows 10 needs to be tweaked for the MSSQL TCP/IP listener to be working.
---
Install MSSQL 2017 Express as usual. After the installation, assuming with default path, we need to enable a new app in Windows Firewall.

* Press META key and then type "firewall" and run "Allow an App through Windows Firewall".
* In the Windows Firewall click _Change Settings._
* Still there, Click _Allow another app...._
* In the Program dialog box, select This program path. Click Browse, and navigate to the instance of SQL Server that you want to access through the firewall, and then click Open. By default, SQL Server is at `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Sqlservr.exe`. Click Next.
* In the Action dialog box, select Allow the connection, and then click Next.
* In the Profile dialog box, select any profiles that describe the computer connection environment when you want to connect to the Database Engine, and then click Next.
* In the Name dialog box, type a name and description for this rule, and then click Finish.


Source:

- [Configure a Windows Firewall for Database Engine Access](https://docs.microsoft.com/en-us/sql/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access?view=sql-server-ver15)