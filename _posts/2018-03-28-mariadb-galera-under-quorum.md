---
title: MariaDB Runs While Under Quorum
tags:
  - mariadb
  - mysql
  - debian
categories:
  - database
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/2018/04/database.png
  overlay_image: /assets/2018/04/database.png
---
WSREP will block mysql clients when the sum of nodes below quorum.

```
ERROR 1047 (08S01): WSREP has not yet prepared node for application use
```

This is true with two nodes one garb. To set the remaining surviving node as master:

```
SET GLOBAL wsrep_provider_options='pc.bootstrap=YES';
```

To force the surviving node accept connections:

```
SET GLOBAL wsrep_provider_options='pc.ignore_sb=TRUE';
```
<em>
Warning: Enabling pc.ignore_sb is dangerous in a multi-master setup, due to the aforementioned risk for split-brain situations. However, it does simplify things in master-slave clusters, (especially in cases where you only use two nodes).
</em>

Source:

<https://stackoverflow.com/a/44667776>
