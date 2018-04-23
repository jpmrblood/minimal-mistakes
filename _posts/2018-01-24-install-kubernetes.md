---
title: Install Kubernetes on My PC
tags:
  - kubernetes
  - ubuntu
  - debian
  - snap
  - juju
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2018/01/kubernetes.png
  overlay_image: /assets/2018/01/kubernetes.png
excerpt: Installing Kubernetes via Juju
---

# Prerequisite

Install snapd if you don't have it yet:

```bash
sudo apt install snapd
```

# Install LXD

Install LXD and add current user permission to use LXD.

```bash
$ sudo snap install lxd                                            
$ sudo usermod -a -G lxd <youruser>                                
$ newgrp lxd                            
$ lxc network set lxdbr0 ipv6.address none ipv6.nat false                           
$ /snap/bin/lxd init           
```

# Install Kubernetes

```bash
$ conjure-up kubernetes
```

Done.
