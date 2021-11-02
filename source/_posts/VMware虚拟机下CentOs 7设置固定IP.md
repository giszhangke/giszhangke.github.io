---
title: VMware虚拟机下CentOs 7设置固定IP
categories:
- tool
- VMware
tags:
- VMware
- CentOs
date: 2020-11-02 23:57:59
---

VMware虚拟机下CentOs 7设置固定IP方法

<!-- more -->

# VMware虚拟机下CentOs 7设置固定IP

修改网卡配置

```
[root@centos-1 ~]# vim /etc/sysconfig/network-scripts/ifcfg-ens33

TYPE="Ethernet"
PROXY_METHOD="none"
BROWSER_ONLY="no"
BOOTPROTO="static"
DEFROUTE="yes"
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_FAILURE_FATAL="no"
IPV6_ADDR_GEN_MODE="stable-privacy"
NAME="ens33"
UUID="51308d1c-f725-49d2-a79b-0b4e1733d369"
DEVICE="ens33"
ONBOOT="yes"
IPADDR="192.168.241.142"
GATEWAY="192.168.241.2"
DNS1="192.168.241.2"

```





# 参考资料

1. [VMware ,CentOs 7设置固定IP](https://blog.csdn.net/zsg88/article/details/75095229)

