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

