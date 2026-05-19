---
title: Kibana Data View
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/14-elasticsearch-architecture.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://www.elastic.co/docs/explore-analyze/find-and-organize/data-views
---

# Kibana Data View

## 一句话说明

Kibana Data View 定义 Kibana 要查看和分析哪些 Elasticsearch 数据，是旧版 Index Pattern 术语的现代对应概念。

## 要点

- Data View 可以匹配一个或多个 index、data stream 或 alias。
- Kibana 用 Data View 决定 Discover、Dashboard 等界面可用的字段和时间字段。
- 旧资料里的 Index Pattern 在新版 Kibana 文档中通常应更新为 Data View。
- Data View 只是 Kibana 的分析入口，不等于 Elasticsearch index 本身。

## 关联页面

- [Elasticsearch 架构](elasticsearch-architecture.md)
- [Elasticsearch Shard](elasticsearch-shard.md)

## 待核实

- 具体 Kibana 版本的界面名称和配置入口可能变化，需要看当前 Elastic 文档。
