---
title: Elasticsearch Shard
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/14-elasticsearch-architecture.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://www.elastic.co/docs/deploy-manage/distributed-architecture/clusters-nodes-shards
---

# Elasticsearch Shard

## 一句话说明

Shard 是 Elasticsearch 把一个 index 分散到多个节点上的基本分片单元。

## 要点

- Primary shard 保存数据的主分片。
- Replica shard 是主分片的副本，用于提升可用性和读取能力。
- shard 数量影响写入、查询、恢复、存储和集群管理成本。
- shard 太少可能限制扩展，太多会增加管理开销。

## 关联页面

- [Elasticsearch 架构](elasticsearch-architecture.md)
- [Kibana Data View](kibana-data-view.md)

## 待核实

- shard 规划必须结合数据量、增长速度、查询模式、节点规格和 Elastic 当前版本建议。
