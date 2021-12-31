---
title: elasticsearch_search_in_deepth
categories:
  - NoSQL
  - Elasticsearch
tags:
  - NoSQL
  - Elasticsearch
date: 2021-12-21 21:19:58
---

**摘要**
Elasticsearch查询的要点归纳



<!-- more -->

# 多字符串查询

要获取 `boost` 参数 “最佳” 值，较为简单的方式就是不断试错：设定 `boost` 值，运行测试查询，如此反复。 `boost` 值比较合理的区间处于 `1` 到 `10` 之间，当然也有可能是 `15` 。如果为 `boost` 指定比这更高的值，将不会对最终的评分结果产生更大影响，因为评分是被 [归一化的（normalized）](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_boosting_query_clauses.html#boost-normalization) 。

# 最佳字段

不使用 `bool` 查询，可以使用 `dis_max` 即分离 *最大化查询（Disjunction Max Query）* 。分离（Disjunction）的意思是 *或（or）* ，这与可以把结合（conjunction）理解成 *与（and）* 相对应。分离最大化查询（Disjunction Max Query）指的是： *将任何与任一查询匹配的文档作为结果返回，但只将最佳匹配的评分作为查询的评分结果返回*

# 最佳字段查询调优

`tie_breaker` 参数提供了一种 `dis_max` 和 `bool` 之间的折中选择，它的评分方式如下：

1. 获得最佳匹配语句的评分 `_score` 。
2. 将其他匹配语句的评分结果与 `tie_breaker` 相乘。
3. 对以上评分求和并规范化。

有了 `tie_breaker` ，会考虑所有匹配语句，但最佳匹配语句依然占最终结果里的很大一部分。



`tie_breaker` 可以是 `0` 到 `1` 之间的浮点数，其中 `0` 代表使用 `dis_max` 最佳匹配语句的普通逻辑， `1` 表示所有匹配语句同等重要。最佳的精确值需要根据数据与查询调试得出，但是合理值应该与零接近（处于 `0.1 - 0.4` 之间），这样就不会颠覆 `dis_max` 最佳匹配性质的根本。