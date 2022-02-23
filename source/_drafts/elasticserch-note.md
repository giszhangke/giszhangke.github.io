---
title: elasticserch-note
categories:
  - NoSQL
  - Elasticsearch
tags:
  - NoSQL
  - Elasticsearch
date: 2022-01-17 13:18:02
---

摘要


<!-- more -->

# 深入搜索

## 控制相关度

### 相关度评分背后的理论

对于有些应用场景如日志，归一值不是很有用，要关心的只是字段是否包含特殊的错误码或者特定的浏览器唯一标识符。字段的长度对结果没有影响，禁用归一值可以节省大量内存空间。



### Lucene 的实用评分函数

我们不建议在建立索引时对字段提升权重

[查询时赋予权重](https://www.elastic.co/guide/cn/elasticsearch/guide/current/query-time-boosting.html) 是更为简单、清楚、灵活的选择