---
title: Install Docker in Debian Stretch
tags:
  - docker
  - debian
  - stretch
categories:
  - notes
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2018/02/docker.png
  overlay_image: /assets/2018/02/docker.png
excerpt: Install Docker in Debian Stretch
---
# Install new repository

```bash
sudo apt install apt-transport-https
wget -O- https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add -
echo "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
    $(lsb_release -cs) \
    stable" | sudo tee /etc/apt/sources.list.d/docker.list
```

# Install Docker

```bash
sudo apt update && sudo apt install docker-ce
sudo systemctl reboot
```
