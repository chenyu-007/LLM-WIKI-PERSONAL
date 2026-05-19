---
title: RAG 学习地图
type: synthesis
status: active
updated: 2026-05-16
sources:
  - raw/sources/2026-05-15-rag-original-paper.source.md
  - raw/sources/2026-05-15-rag-survey.source.md
  - raw/sources/2026-05-15-self-rag.source.md
  - raw/sources/2026-05-15-raptor.source.md
  - raw/sources/2026-05-15-graphrag.source.md
---

# RAG 学习地图

## 一句话说明

学习 RAG 时，先掌握基础检索增强生成流程，再学习检索优化、质量评估和高级结构。

## 学习顺序

1. **总概念：** 读 [Retrieval-Augmented Generation](../concepts/retrieval-augmented-generation.md)，理解 RAG 解决的是外部知识接入问题。
2. **基础流程：** 读 [RAG Pipeline](../concepts/rag-pipeline.md)，区分离线索引和在线问答。
3. **索引基础：** 读 [Chunking](../concepts/chunking.md)、[Embedding](../concepts/embedding.md) 和 [向量数据库](../concepts/vector-database.md)，理解资料如何变成可检索对象。
4. **检索优化：** 读 [Hybrid Search](../concepts/hybrid-search.md) 和 [Reranker](../concepts/reranker.md)，理解为什么只靠向量检索不够。
5. **质量问题：** 读 [为什么 RAG 仍然会幻觉](../questions/why-rag-still-hallucinates.md)，学会从资料、切块、检索、排序、上下文和生成逐层排查。
6. **方案边界：** 读 [RAG 和 Fine-tuning 怎么选](../questions/rag-vs-fine-tuning.md)，避免把 RAG 当成万能方案。
7. **高级方向：** 再看 Self-RAG、RAPTOR 和 GraphRAG，理解自适应检索、层级检索和图结构检索。

## 三个阶段

### Naive RAG

基础版本：切块、向量化、向量检索、把 top-k 塞进 Prompt，让模型回答。

适合入门和小规模资料，但容易遇到检索不准、上下文噪声和引用不稳。

### Advanced RAG

在基础流程上加入查询改写、Hybrid Search、Reranker、上下文压缩、引用校验和评估。

这是多数实用系统真正需要掌握的层次。

### Modular RAG

把 RAG 拆成可组合模块，加入路由、多跳检索、工具调用、图谱、记忆和反馈循环。

适合复杂业务系统，但维护成本明显更高。

## 代表性高级方向

- **Self-RAG：** 让模型自适应判断是否需要检索，并评价检索结果和回答是否被支持。
- **RAPTOR：** 用递归聚类和摘要构建树状索引，适合长文档和层级语义。
- **GraphRAG：** 用实体图和社区摘要回答面向整个语料的全局问题。

## 对本地知识库的启发

当前 `llm-wiki` 阶段不急着上向量库。更合理的顺序是：

1. 先把 Markdown 页面、来源记录、索引和日志维护好。
2. 页面数量变多后，先用全文搜索和结构化索引。
3. 当关键词搜索不够用时，再考虑 Embedding 和 Hybrid Search。
4. 当检索结果多而杂时，再加入 Reranker。
5. 只有出现全局综述、多跳关系和大规模语料问题时，再考虑 GraphRAG 或复杂 RAG。

## 关联页面

- [LLM Wiki](../concepts/llm-wiki.md)
- [RAG 原始论文](../sources/rag-original-paper.md)
- [RAG 大模型综述](../sources/rag-survey.md)
- [Self-RAG](../sources/self-rag.md)
- [RAPTOR](../sources/raptor.md)
- [GraphRAG](../sources/graphrag.md)
- [Retrieval-Augmented Generation](../concepts/retrieval-augmented-generation.md)
- [RAG Pipeline](../concepts/rag-pipeline.md)
- [向量数据库](../concepts/vector-database.md)
- [RAG 和 Fine-tuning 怎么选](../questions/rag-vs-fine-tuning.md)
- [为什么 RAG 仍然会幻觉](../questions/why-rag-still-hallucinates.md)

## 待核实

- 具体 RAG 框架、向量数据库、Embedding 模型和评估工具变化很快，进入实现阶段时需要重新检索最新文档。
