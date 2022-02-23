---
title: MySQL锁及使用场景
categories: 
- 数据库
- MySQL
tags:
  - MySQL
date: 2022-02-23 22:35:09
---

MySQL的锁分为表锁、行锁、间隙锁（Gap锁）、意向锁、共享锁、排他锁、悲观锁、乐观锁

<!-- more -->

# 按不度角度分类

## 锁粒度

- 行锁
- 表锁
- 页锁

## 算法

- Record Lock
- Gap Lock
- Next-key Lock

## 实现机制

- 悲观锁
- 乐观锁

## 兼容性

- 排它锁
- 共享锁
- 意向锁

# 锁的应用场景



# 参考资料

1.[MySQL-深入浅出锁分类及实现原理](https://zhuanlan.zhihu.com/p/296545804)

