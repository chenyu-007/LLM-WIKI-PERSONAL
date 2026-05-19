---
title: Hybrid Search
type: concept
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-rag-survey.source.md
---

# Hybrid Search

## 一句话说明

Hybrid Search 是把向量检索和关键词检索结合起来，提高 RAG 召回稳定性的检索策略。

## 要点

- 向量检索擅长语义相似，关键词检索擅长精确匹配。
- 技术文档、代码库、产品资料和论文中常有术语、编号、函数名、错误码，仅靠向量检索容易漏召回。
- Hybrid Search 通常先分别召回候选，再融合分数或合并结果。
- Hybrid Search 之后常接 Reranker，让更强的模型重新排序候选片段。

## 适合场景

- 专有名词很多的文档。
- 包含 API、代码、错误码、论文术语的资料。
- 用户问题既有自然语言描述，也有精确关键词。
- 单纯向量检索经常漏掉明显答案。

## 不适合场景

- 资料非常少，全文直接读取即可。
- 搜索需求很简单，关键词检索已经足够。
- 没有评估集，无法判断混合权重是否真的改善效果。

## 关联页面

- [Embedding](embedding.md)
- [Reranker](reranker.md)
- [RAG Pipeline](rag-pipeline.md)
- [RAG 学习地图](../syntheses/rag-learning-map.md)

## 待核实

- 不同向量数据库和搜索引擎对 hybrid search 的实现不同，具体参数需要按工具文档确认。
