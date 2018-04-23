---
title: VirtualBox After Clone
tags:
  - virtualbox
  - guest
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: VirtualBox on a new machine from clone.
---

After cloning a VM template, we need to change things to make us stay out of trouble.

SSH to the machine and do these things.
# Conventions

```bash
export NEW_HOSTNAME='newhost0'
```

# Machine ID

Change machine ID.

```bash
sudo apt-get dist-upgrade
sudo rm /var/lib/dbus/machine-id
sudo rm /etc/machine-id
sudo systemd-machine-id-setup
sudo ln -s /etc/machine-id /var/lib/dbus/
```

# Hostname

```bash
echo "127.0.0.1 $NEW_HOSTNAME" | sudo tee -a /etc/hosts
sudo hostnamectl set-hostname $NEW_HOSTNAME
```
