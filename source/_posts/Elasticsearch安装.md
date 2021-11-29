---
title: Elasticsearch安装
categories:
  - NoSQL
  - Elasticsearch
tags:
  - NoSQL
  - Elasticsearch
date: 2021-11-25 18:02:49
---

**摘要**

Elasticsearch单节点安装，启动，验证

<!-- more -->



# 安装

## 安装环境前置条件

| 软件          | 版本   | 备注                                  |
| ------------- | ------ | ------------------------------------- |
| Centos        | 7.6    | 查看系统版本`cat /etc/redhat-release` |
| JDK           | 1.8    |                                       |
| Elasticsearch | 5.6.16 |                                       |

## 安装步骤

1. 下载安装包

   ```bash
   curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.6.16.tar.gz
   ```

2. 解压缩

   `tar -xvf elasticsearch-5.6.16.tar.gz`

3. 添加用户组和用户

   `groupadd es && useradd -g es es`
   
4. 给新增用户添加安装目录权限
   
   ``chown -R es:es [安装目录]``
   
   例如：
   
   ``chown -R es:es /data/elasticsearch/elasticsearch-5.6.16``
   
   

# 启动

1. 切换到es用户

   ``su es``

2. 启动elasticsearch

   ``cd [安装目录] && ./bin/elasticsearch``

   例如

   ``cd /data/elasticsearch/elasticsearch-5.6.16 && ./bin/elasticsearch``

   如果正常运行，打印输出如下

   ![img](es_run_print.png)

   

# 验证

新打开一个终端窗口，输入``curl http://localhost:9200/?pretty`` ,  正常情况会输出类似结果

```json
{
  "name" : "GzSfhee",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "4cVKpiWgQlSE9OhC7cYzcA",
  "version" : {
    "number" : "5.6.16",
    "build_hash" : "3a740d1",
    "build_date" : "2019-03-13T15:33:36.565Z",
    "build_snapshot" : false,
    "lucene_version" : "6.6.1"
  },
  "tagline" : "You Know, for Search"
}
```

可以通过参数改变集群名称和节点名称

```./bin/elasticsearch -Ecluster.name=my_cluster_name -Enode.name=my_node_name```

如果想把 Elasticsearch 作为一个守护进程在后台运行，那么可以在后面添加参数 `-d`

# 常见问题

1. 启动后只能本机访问

   - 用``exit``命令退出es用户
   
   - 修改``network.host``属性，例如改为``0.0.0.0``不做访问ip限制 
   
     ``vim [安装目录]/config/elasticsearch.yml``

   - 编辑``/etc/sysctl.conf``文件，修改或新增属性``vm.max_map_count=655360``，执行``sysctl -p``命令使修改生效
   
   - 关闭防火墙或者开放elasticsearch服务端口`9200`
   
   - 切换回es用户``su es``重新启动elasticsearch就可以远程访问了
   
   

# 参考资料

1. [Elasticsearch Reference - Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/_installation.html)
2. [ES安装教程详解](https://blog.csdn.net/he19970408/article/details/107359861/)
3. [Linux 用户和用户组管理](https://www.runoob.com/linux/linux-user-manage.html)
4. [Centos防火墙设置与端口开放的方法](https://blog.csdn.net/u011846257/article/details/54707864)