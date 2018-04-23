---
title: Installing OpenJDK for Servers
tags:
  - java
  - jdk
  - jvm
  - headless
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/2018/04/java2.png
  overlay_image: /assets/2018/04/java2.png
excerpt: Installing OpenJDK for Servers
---

Everyone loves bloated thing. :P
I am a hipster.

# Conventions

```bash
export JAVA_VERSION=9
```

Now range: 7, 8, 9, 10!

# Install OpenJDK

```bash
sudo apt install openjdk-$JAVA_VERSION-jdk-headless
```

Remember, this is headless, means no GUI libs.
