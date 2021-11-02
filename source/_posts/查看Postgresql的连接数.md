---
title: PostgreSQL连接数查询
categories: database
tags:
  - postgresql
date: 2021-11-02 23:57:59
---

查看postgresql的连接数、最大连接数限制、保留的连接数

<!--more-->

查看postgresql的连接数：

```select * from pg_stat_activity;```

查看最大连接数限制：

```show max_connections;```


查看为超级用户保留的连接数：

```show superuser_reserved_connections ; ```

# 参考资料
 1. [查看Postgresql的连接数](https://www.cnblogs.com/Smart_Joe/archive/2012/06/14/2549355.html)