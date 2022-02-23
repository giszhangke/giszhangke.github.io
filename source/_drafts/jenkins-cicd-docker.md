---
title: jenkins-cicd-docker
categories: 
- Tool
- Jenkins
tags:
  - Jenkins
date: 2022-02-15 16:00:08
---


Jenkins docker容器重启其他docker容器

<!-- more -->

# 目标



# 步骤

挂载宿主机docker目录到Jenkins容器上

```
 -v /var/run/docker.sock:/var/run/docker.sock 
 -v /usr/bin/docker:/usr/bin/docker 
 -v /usr/lib64/libltdl.so.7:/usr/lib/x86_64-linux-gnu/libltdl.so.7
```


以root用户启动Jenkins容器

```
-u root
```



# 问题

## ....libltdl.so.7: cannot open shared object file...

进入容器内部安装对应的依赖

`````
apt-get update
apt-get install -y libltdl7
`````





# 参考资料

1. [](https://blog.csdn.net/y42775jp_lm/article/details/81436317)

2. [](https://github.com/moby/moby/issues/37531)

3. [](https://www.jianshu.com/p/8b72eece7df8)