---
title: Spring Boot Disables Security
tags:
  - java
  - spring
  - security
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/the-most-terrifying.png
  overlay_image: /assets/the-most-terrifying.png
excerpt: Change a web service endpoint.
---
Developing project with security is quite hassle if we are developing the functionality. In order to run without Spring Security:

```bash
java -Dmanagement.security.enabled=false -Dsecurity.ignored="/**" springboot-app.jar
```

It means, setup:

```yaml
management.security.enabled: false
security.ignored: "/**"
```

SOURCE:
[stackoverflow](https://stackoverflow.com/questions/23894010/spring-boot-security-disable-security)

Now, do other thing as usual.