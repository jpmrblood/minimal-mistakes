---
title: Installing Oracle Java 10 JDK on Debian Stretch
tags:
  - debian
  - stretch
  - oracle
  - java
  - jdk
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/2018/04/java2.png
  overlay_image: /assets/2018/04/java2.png
excerpt: Installing Oracle Java 10 JDK on Debian Stretch
---

This is how we install Oracle Java. It uses different repository than JDK9 and JDK8

# Import key
```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 73C3DB2A
```

# Install Java
```bash
echo "deb http://ppa.launchpad.net/linuxuprising/java/ubuntu xenial main " | sudo tee -a /etc/apt/sources.list.d/linux-uprising_java.list
echo "deb http://ppa.launchpad.net/linuxuprising/java/ubuntu xenial main " | sudo tee -a /etc/apt/sources.list.d/linux-uprising_java.list
sudo apt update
sudo apt install oracle-java10-installer
```


Reference:

[“Linux Uprising” team Oracle Java](https://launchpad.net/~linuxuprising/+archive/ubuntu/java)
[Option 1: Easy Installation (PPA)](https://stackoverflow.com/a/49507161)
