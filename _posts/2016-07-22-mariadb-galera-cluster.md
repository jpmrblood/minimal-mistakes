---
title: MariaDB + Galera Cluster + HAProxy
tags:
 - mariadb
 - galera
 - haproxy
 - debian
 - linux
categories:
 - admin
 - linux
 - review
---

![HA Proxy encapsulate a Galera cluster for High-Availability solution.](/assets/haproxy-galera-1.png){: .align-center}

### Configuration

There are 4 servers.

HAProxy, 2 nodes:

* IP 1: 192.168.1.12
* IP 2: 192.168.101.1

MariaDB, 3 nodes: (for quorum)

* MariaDB1 (192.168.101.10)
* MariaDB2 (192.168.101.11)
* MariaDB3 (192.168.101.12)

# Installing MariaDB

Takes three steps:

* setup repository
* add repo keyring
* install MariaDB


## Adding MariaDB Debian repository

### Alternative I

~~~console
$ cat > /etc/apt/sources.list.d/mariadb.list << EOF
# MariaDB 10.1 repository list - created 2016-07-22 08:52 UTC
# http://downloads.mariadb.org/mariadb/repositories/
deb [arch=amd64,i386] http://mariadb.biz.net.id/repo/10.1/debian jessie main
deb-src http://mariadb.biz.net.id/repo/10.1/debian jessie main
EOF
~~~

### Alternative II

~~~console
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository 'deb [arch=amd64,i386] http://mariadb.biz.net.id/repo/10.1/debian jessie main'
~~~

## Add GPG keyring

Add MariaDB Debian repository keyring

~~~console
$ sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 0xcbcb082a1bb943db
~~~

## Install MariaDB

Installing MariaDB server will also automatically install RSYNC and Galera Cluster

~~~console
$ sudo apt-get install mariadb-server
~~~

# Configuring Galera

There are three steps to up the Galera cluster:

* configure each nodes for galera.
* run one node as the first in node.
* run the two other nodes.

## MariaDB1, MariaDB2, MariaDB3

Do this on all the MariaDB servers.

~~~console
$ cat > /etc/mysql/conf.d/galera.cnf << EOF
[mysqld]
#mysql settings
binlog_format=ROW
default-storage-engine=innodb
innodb_autoinc_lock_mode=2
innodb_doublewrite=1
query_cache_size=0
query_cache_type=0
bind-address=0.0.0.0

#galera settings
wsrep_on=ON
wsrep_provider=/usr/lib/galera/libgalera_smm.so
wsrep_cluster_name="apakek_cluster"
wsrep_cluster_address=gcomm://192.168.101.10,192.168.101.11,192.168.101.12
wsrep_sst_method=rsync
EOF
~~~

You can creatively change the name `galera.cnf` into `galerbiji.cnf` or any name that
your brain could summon.

## MariaDB1

For simplicity, lets assume we want to make MariaDB1 as the first master.

### Debian with `systemd` (e.g. Jessie)

~~~console
$ sudo /usr/bin/galera_new_cluster
~~~

### Debian with other sysinit

~~~console
sudo service mysql start --wsrep-new-cluster
~~~

## Final check

To check how many node run on the cluster.

~~~console
$ sudo mysql --defaults-file=/etc/mysql/debian.cnf -e 'SELECT VARIABLE_VALUE as "cluster size" FROM INFORMATION_SCHEMA.GLOBAL_STATUS WHERE VARIABLE_NAME="wsrep_cluster_size"'
+--------------+
| cluster size |
+--------------+
| 1            |
+--------------+
~~~

## MariaDB2, MariaDB3

The rest of the nodes.

### Debian with `systemd` (e.g. Jessie)

~~~console
$ sudo systemctl start mysql
~~~

### Debian with other sysinit

~~~console
$ sudo service mysql start
~~~

## Final check

Final check how many node run on the cluster.

~~~console
$ sudo mysql --defaults-file=/etc/mysql/debian.cnf -e 'SELECT VARIABLE_VALUE as "cluster size" FROM INFORMATION_SCHEMA.GLOBAL_STATUS WHERE VARIABLE_NAME="wsrep_cluster_size"'
+--------------+
| cluster size |
+--------------+
| 3            |
+--------------+
~~~

## Excercise

Create admin users that could be accessed via network is left as an excercise
to the reader.

# HAProxy

Create a user for HAProxy. This user is used to ping check health status.

~~~console
$ sudo mysql --defaults-file=/etc/mysql/debian.cnf -e "CREATE USER 'haproxy'@'192.168.101.1'"
~~~

Append these lines in `/etc/haproxy/haproxy.cfg` file.

~~~
# Load Balancing for Galera Cluster
listen galera 192.168.1.12:3306
     balance source
     mode tcp
     option tcpka
     option mysql-check user haproxy
     server node1 192.168.101.10:3306 check weight 1
     server node2 192.168.101.11:3306 check weight 1
     server node2 192.168.101.12:3306 check weight 1
~~~

Restart HAProxy.

~~~console
$ sudo service haproxy restart
~~~

Done.

# Optimization

There are things that can be done to optimize:

* Replacing HAProxy with hardware load-balancer .
* Setup HAProxy as gateway/interface to application in each node.
![HAProxy per instance](/assets/haproxy-galera-per-apps.png)
* Use cookbook like Chef, Puppet or Ansible to automate this process.

# Further Read

* [HAProxy — Galera Cluster Documentation](http://galeracluster.com/documentation-webpages/haproxy.html)
* [Node Failure and Recovery — Galera Cluster Documentation](http://galeracluster.com/documentation-webpages/recovery.html)
* [Starting the Cluster — Galera Cluster Documentation](http://galeracluster.com/documentation-webpages/startingcluster.html)
* [How to Deploy Galera Cluster for MySQL using Docker Containers :: Severalnines](http://severalnines.com/blog/how-deploy-galera-cluster-mysql-using-docker-containers)
* [MariaDB 10.1 Galera Cluster on Debian 8 Jessie - Sprinternet Blog](https://blog.sprinternet.at/2016/03/mariadb-10-1-galera-cluster-on-debian-8-jessie/)
* [MySQL :: MySQL 5.5 Reference Manual :: 6.3.2 Adding User Accounts](https://dev.mysql.com/doc/refman/5.5/en/adding-users.html)
* [Planet MySQL - Archives - The Galera installation guide for dummies.](https://planet.mysql.com/entry/?id=282416)
* [WordPress JP: Installing MariaDB – Wannabe Exceptional](https://staff.blog.ui.ac.id/jp/2016/05/10/wordpress-jp-installing-mariadb/)
