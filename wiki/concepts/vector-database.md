---
title: 向量数据库
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/07-retrieval-augmented-generation.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://docs.pinecone.io/guides/get-started/overview
---

# 向量数据库

## 一句话说明

向量数据库用于存储向量表示，并按相似度检索最接近查询向量的对象，是 RAG 系统常见的检索组件。

## 要点

- 向量数据库存的是向量及其元数据，不是直接“理解”文档。
- 在 RAG 中，文档 chunk 通常先由 [Embedding](embedding.md) 模型转成向量，再写入向量数据库。
- 查询时，用户问题也会转成向量，用相似度搜索找相关 chunk。
- 元数据过滤用于限定集合、权限、时间、来源或文档类型。
- 向量数据库只是 RAG 的一环，不替代资料清洗、chunk 设计、重排、引用和评估。

## 常见误区

- 误区：上了向量数据库就等于有了 RAG。
- 现实：没有高质量资料和检索评估，向量库只会更快地召回噪声。
- 误区：相似度最高的片段一定最适合回答。
- 现实：还需要考虑关键词、权限、时效、上下文完整性和重排。

## 关联页面

- [Retrieval-Augmented Generation](retrieval-augmented-generation.md)
- [RAG Pipeline](rag-pipeline.md)
- [Embedding](embedding.md)
- [Hybrid Search](hybrid-search.md)
- [Reranker](reranker.md)

## 待核实

- Pinecone、Milvus、Weaviate、Qdrant、Elasticsearch 等工具的索引算法、过滤语义和运维能力不同，选型时必须看当前官方文档和实际数据规模。
