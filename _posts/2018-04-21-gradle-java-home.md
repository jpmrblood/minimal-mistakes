---
title: Gradle Select Java Version
tags:
  - gradle
  - java
  - home
categories:
  - java
header:
  overlay_filter: "0.5"
  overlay_color: "#74b9ff"
  teaser: /assets/2018/04/gradle.png
  overlay_image: /assets/2018/04/gradle.png
---

Sometimes we need so many version of Java.

# Conventions

```bash
export JAVA_HOME=/usr/lib/jvm/java-9-openjdk-amd64

```

Change the version with the one that you desire.

# Run

On our Gradle project:

```bash
$  ./gradlew -Dorg.gradle.java.home=$JAVA_HOME
```
