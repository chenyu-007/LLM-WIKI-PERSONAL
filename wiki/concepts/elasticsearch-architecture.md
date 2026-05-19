---
title: Elasticsearch 架构
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/14-elasticsearch-architecture.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://www.elastic.co/docs/deploy-manage/distributed-architecture/clusters-nodes-shards
---

# Elasticsearch 架构

## 一句话说明

Elasticsearch 可以从 Cluster、Node、Index、Shard、Document 这几层理解，它面向搜索、日志和文档分析，不是关系型数据库的直接替代品。

## 要点

- Cluster 是一组共同工作的 Elasticsearch 节点。
- Node 是集群中的一个 Elasticsearch 实例。
- Index 是一组可搜索文档的逻辑集合，但只适合作为入门类比，不应严格等同关系型表。
- Document 是可索引和搜索的 JSON 文档。
- [Elasticsearch Shard](elasticsearch-shard.md) 是索引的分片单元，影响容量、可用性和查询并发。
- Mapping 定义字段类型和索引方式，是搜索质量和存储成本的重要基础。

## 与监控系统的边界

- Elasticsearch 适合日志、文档、全文检索和分析。
- Prometheus 更适合时序指标采集、查询和告警。
- 二者可以配合，但不要把日志搜索和指标监控混成一个问题。

## 关联页面

- [Elasticsearch Shard](elasticsearch-shard.md)
- [Kibana Data View](kibana-data-view.md)
- [Prometheus 和 Elasticsearch 怎么区分](../syntheses/prometheus-vs-elasticsearch.md)

## 待核实

- Elasticsearch 版本变化会影响术语和默认行为，尤其是旧资料中的 type、index pattern 等说法。
