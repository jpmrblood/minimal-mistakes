---
title: CAS Redis Ticket Storage
tags:
  - java
  - cas
  - idp
categories:
  - cas
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/2018/04/java2.png
  overlay_image: /assets/2018/04/java2.png
excerpt: CAS Redis Ticket Storage
---

# Conventions

```bash
export REDIS_PASSWORD=`pwgen 32 1`
export REDIS_SERVER=192.0.2.10
export CAS_SRC_DIR=`pwd` # somewhere
```

Yes, I assume we are on root directory of our CAS Gradle overlay.

# Setup Redis Server

```bash
sudo apt install redis-server
```

Disable bind to localhost only: (default Debian Stretch install)

```bash
sudo sed -i 's/^bind/#bind/'
```

Add Redis access password:

```bash
echo "requirepass $REDIS_PASSWORD" | sudo tee -a /etc/redis/redis.conf
```

Restart Redis:

```bash
sudo /etc/init.d/redis-server restart
```

# Setup CAS Dependency
Add to cas' build.gradle CAS Redis dependency.

```gradle
compile "org.apereo.cas:cas-server-support-redis-ticket-registry:${project.'cas.version'}"
```


So, file becomes `$CAS_SRC_DIR/cas/build.gradle`:

```gradle
// ...
dependencies {
    compile "org.apereo.cas:cas-server-webapp-jetty:${project.'cas.version'}@war"
    compile "org.apereo.cas:cas-server-support-redis-ticket-registry:${project.'cas.version'}"
    if (!project.hasProperty('bootiful')) {
        // Other dependencies may be listed here...
    } else {
        println "Running CAS in Bootiful mode; all dependencies except the CAS web application are ignored."
    }
}
// ...
```

Rebuild CAS:

```bash
./build clean build
```

# Setup CAS configuration

Append to CAS configuration:

```bash
cat >> etc/cas/config/cas.properties << EOF
# Ticket granting
cas.tgc.crypto.encryption.key=wSQUZVGqXGzJJZYa89654xIf_U8mSughk8f9tlo6Zts
cas.tgc.crypto.signing.key=GmARoc8Ej2WnAhjAUadaNhjCKpif60M8MqfL-q4IymQo1KyutBulZGi_FB3ZZHieTi27ButDEtBB8wFxfvuGLA

# REDIS Ticket
cas.ticket.registry.redis.host=$REDIS_SERVER
cas.ticket.registry.redis.database=0
cas.ticket.registry.redis.port=6379
cas.ticket.registry.redis.password=$REDIS_PASSWORD

EOF
```

Move to CAS configuration directory:

```bash
./build copy
```

You could restart CAS, but CAS have an ability to read configuration change on-the-fly.

Run CAS if it isn't run:

```bash
./build run
```

Or

```bash
java -jar cas/build/libs/cas.war
```

## Test

If doing it right

```bash
redis-cli
127.0.0.1:6379> AUTH nee8oohiNg3WiWoetapha3iwae9giej3
OK
127.0.0.1:6379> CLIENT LIST
id=86 addr=192.0.2.11:52512 fd=6 name= age=56 idle=29 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 events=r cmd=ping
id=87 addr=127.0.0.1:56782 fd=7 name= age=5 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=32768 obl=0 oll=0 omem=0 events=r cmd=client

```

# Reference

[Redis Ticket Registry](https://apereo.github.io/cas/5.2.x/installation/Redis-Ticket-Registry.html)
[CAS Properties: Redis Ticket Registry](https://apereo.github.io/cas/5.2.x/installation/Configuration-Properties.html#redis-ticket-registry)
