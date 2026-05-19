---
title: Prometheus 和 Elasticsearch 怎么区分
type: synthesis
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/14-elasticsearch-architecture.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://www.elastic.co/docs/deploy-manage/distributed-architecture/clusters-nodes-shards
---

# Prometheus 和 Elasticsearch 怎么区分

## 一句话说明

Prometheus 更偏时序指标监控和告警，Elasticsearch 更偏日志、文档搜索和分析。

## 对比

| 维度 | Prometheus | Elasticsearch |
| --- | --- | --- |
| 主要数据 | metrics | logs / documents / events |
| 查询重点 | 时间序列、聚合、告警 | 全文检索、过滤、聚合分析 |
| 常见问题 | CPU、内存、QPS、延迟 | 错误日志、请求链路、文档检索 |
| 展示工具 | Grafana 常见 | Kibana 常见 |

## 使用建议

- 系统健康和告警优先考虑 Prometheus。
- 日志检索、错误排查和文档分析优先考虑 Elasticsearch。
- 复杂可观测性系统通常会同时使用 metrics、logs 和 traces，而不是只选一个。

## 关联页面

- [Elasticsearch 架构](../concepts/elasticsearch-architecture.md)
- [Kibana Data View](../concepts/kibana-data-view.md)

## 待核实

- Prometheus 细节页尚未建立；后续如果学习监控体系，应单独补充 Prometheus 概念页。
