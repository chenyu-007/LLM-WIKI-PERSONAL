---
title: Embedding
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/sources/2026-05-15-rag-survey.source.md
  - raw/inbox/youdao/approved-2026-05-15/07-retrieval-augmented-generation.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://developers.openai.com/api/docs/guides/embeddings
---

# Embedding

## 一句话说明

Embedding 是把文本、图片或其他对象转换成向量表示的方法，RAG 常用它做语义相似度检索。

## 要点

- 在文本 RAG 中，Embedding 通常把 query 和 chunk 都映射到向量空间。
- 向量距离越近，通常表示语义越相似。
- Embedding 本身只产生向量；向量的存储、过滤和近似最近邻搜索通常由 [向量数据库](vector-database.md) 或搜索引擎承担。
- Embedding 检索擅长语义相近但措辞不同的问题。
- Embedding 检索不一定擅长精确匹配编号、专有名词、代码符号和短关键词。
- 因此成熟 RAG 常把向量检索和关键词检索组合成 Hybrid Search。

## 常见误区

- 误区：用了 Embedding 就等于做了高质量 RAG。
- 现实：Embedding 只是检索的一环，资料清洗、chunk、元数据、重排和评估同样关键。
- 误区：Embedding 模型越新，RAG 一定越好。
- 现实：Embedding 模型需要和语言、领域、资料结构、查询类型匹配。

## 适用范围

适合：

- 基于语义相似度检索文档片段。
- 处理自然语言问答、概念解释和资料归纳。
- 作为第一轮粗召回模块。

不适合：

- 单独承担精确关键词、ID、代码、公式和表格查询。
- 替代权限控制、来源管理或事实校验。

## 关联页面

- [RAG Pipeline](rag-pipeline.md)
- [向量数据库](vector-database.md)
- [Hybrid Search](hybrid-search.md)
- [Reranker](reranker.md)
- [RAG 学习地图](../syntheses/rag-learning-map.md)

## 待核实

- 具体 Embedding 模型选择会随厂商和开源模型更新变化，需要在选型时重新比较。
