---
title: Oracle 12d Pluggable Database
tags:
  - oracle
  - database
categories:
  - notes
header:
  overlay_filter: "0.5"
  overlay_color: "#000"
  teaser: /assets/2018/04/java2.png
  overlay_image: /assets/2018/04/java2.png
excerpt: Oracle 12d Pluggable Database
---
Application sometimes stop:

```
java.sql.SQLRecoverableException: ORA-01033: ORACLE initialization or shutdown in progress

        at oracle.jdbc.driver.T4CTTIoer11.processError(T4CTTIoer11.java:494)
        at oracle.jdbc.driver.T4CTTIoer11.processError(T4CTTIoer11.java:441)
        at oracle.jdbc.driver.T4CTTIoer11.processError(T4CTTIoer11.java:436)
        at oracle.jdbc.driver.T4CTTIoauthenticate.processError(T4CTTIoauthenticate.java:546)
        at oracle.jdbc.driver.T4CTTIfun.receive(T4CTTIfun.java:623)
        at oracle.jdbc.driver.T4CTTIfun.doRPC(T4CTTIfun.java:252)
        at oracle.jdbc.driver.T4CTTIoauthenticate.doOSESSKEY(T4CTTIoauthenticate.java:519)
        at oracle.jdbc.driver.T4CConnection.logon(T4CConnection.java:615)
        at oracle.jdbc.driver.PhysicalConnection.connect(PhysicalConnection.java:688)
        at oracle.jdbc.driver.T4CDriverExtension.getConnection(T4CDriverExtension.java:39)
        at oracle.jdbc.driver.OracleDriver.connect(OracleDriver.java:691)
        at org.apache.tools.ant.taskdefs.JDBCTask.getConnection(JDBCTask.java:370)
        at org.apache.tools.ant.taskdefs.SQLExec.getConnection(SQLExec.java:940)
        at org.apache.tools.ant.taskdefs.SQLExec.execute(SQLExec.java:612)
```

Well, this sometimes because we setup the new Pluggable database in Oracle 12c as our database.

Need to login to the DB and do:

```
ALTER PLUGGABLE DATABASE omnidev OPEN;
```