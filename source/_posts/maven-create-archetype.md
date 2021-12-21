---
title: 创建Maven代码骨架
categories:
  - Tool
  - Maven
tags:
  - Maven
date: 2021-12-14 13:34:58
---

根据已有Maven项目生成Maven骨架代码

<!-- more -->

# 前置条件

1. 已经安装好Maven
2. 已经创建好一个Maven项目

3. 设项目根目录为RootPath

# 步骤

## 安装依赖

进入RootPath，执行命令 ``mvn install``

## 生成骨架代码

执行命令 ``mvn archetype:create-from-project``

创建完成后，会在RootPath生成一个``target``文件夹，内容如下图1所示

![img](target-archetype.png)

<center>图1. 生成的代码骨架</center>