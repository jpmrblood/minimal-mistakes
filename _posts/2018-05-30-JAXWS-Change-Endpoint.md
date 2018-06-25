---
title: JAX WS Change Endpoint
tags:
  - java
  - jaxws
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/2018/04/java2.png
  overlay_image: /assets/2018/04/java2.png
excerpt: Change a web service endpoint.
---
Consider that we defined a web service:

```java
MyServicePortType service = new MyServiceService().getMyServicePortType();
```

Normally, we would go on and put the param at the service. Not yet, change the address first:

```java
BindingProvider bindingProvider = (BindingProvider) service;

bindingProvider.getRequestContext().put(
  BindingProvider.ENDPOINT_ADDRESS_PROPERTY,
  "http://new.server/endpoint"
);
```

SOURCE:
[stackoverflow](https://stackoverflow.com/a/3569291)

Now, do other thing as usual.