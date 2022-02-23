---
title: Docker容器和宿主机通信
categories:
  - 容器化
  - docker
tags:
  - docker
date: 2021-12-31 18:20:42
---



docker和宿主机之前有三种网络通信模式：

- none

- host

- bridge  (默认)

  

<!-- more -->



# 问题由来

在测试服务器上安装好Docker后，设置端口映射并启动容器，发现在PC访问不了服务



# 原因分析

经查发现容器和宿主机之间通信异常
宿主机上Docker的网卡是 docker0， 对应的ip是``172.17.0.1``
docker容器内部的ip是``172.17.0.2``
但是主机``ping``不通``172.17.0.2``
容器也``ping``不通``172.17.0.1``

# 解决方案

先执行命令

````
service docker stop
yum install bridge-utils
brctl addbr br0
ip addr add 172.16.0.1/24 dev br0
ip link set dev br0 up
# 在daemon.json中增加 "bridge":"br0"
vim /etc/docker/daemon.json
service docker start
````

再重启docker容器



