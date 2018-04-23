---
title: Setup A Headless Server for Android Project
tags:
  - Android
  - Studio
  - project
  - gradle
categories:
  - linux
  - android
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  teaser: /assets/2017/02/android-recharged.png
  overlay_image: /assets/2017/02/android-recharged.png
excerpt: Creating a headless server used for compiling an Android Project
  created by Android Studio
---
# Prerequisites

```
export ANDROID_HOME=$HOME/Android
export PATH=$ANDROID_HOME/tools:$PATH

echo "export ANDROID_HOME=\$HOME/Android" >> ~/.bashrc
echo "export PATH=\$ANDROID_HOME/tools:\$PATH" >> ~/.bashrc
```

# Java SDK

```
echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | sudo tee /etc/apt/sources.list.d/webupd8team-java.list
echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | sudo tee -a /etc/apt/sources.list.d/webupd8team-java.list
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886
sudo apt-get update
sudo apt-get install -y oracle-java8-installer
```

# Library Prerequisites

```
sudo apt-get install -y libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5
sudo apt-get install -y lib32z1
```

# Install Android Tools

```
mkdir $ANDROID_HOME
wget https://dl.google.com/android/repository/tools_r25.2.3-linux.zip
unzip tools_r25.2.3-linux.zip -d $ANDROID_HOME
```
# Install Android SDK

## ANDROID API 21, 21.1.2

```
android update sdk --no-ui --all  --filter 1,2,16,37,166
```

# Some Quirks

```
echo count=0 > ~/.android/repositories.cfg
```
