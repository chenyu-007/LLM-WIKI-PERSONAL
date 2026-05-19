---
title: RAG Pipeline
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/sources/2026-05-15-rag-original-paper.source.md
  - raw/sources/2026-05-15-rag-survey.source.md
  - raw/inbox/youdao/approved-2026-05-15/07-retrieval-augmented-generation.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
---

# RAG Pipeline

## 一句话说明

RAG Pipeline 是把外部资料转化为可检索上下文，并把检索结果交给 LLM 生成答案的一组处理步骤。

## 要点

- RAG Pipeline 通常分为离线索引阶段和在线问答阶段。
- 离线阶段负责资料清洗、切块、向量化、索引和元数据保存。
- 在线阶段负责查询理解、检索、重排、上下文组装、生成和结果校验。
- Advanced RAG 会在检索前后加入查询改写、混合检索、重排、上下文压缩和引用校验。
- Modular RAG 会把各步骤拆成可替换模块，例如路由、多跳检索、工具调用和反馈循环。

## 两个阶段

### 离线索引

```text
文档收集 → 清洗 → 切块 → Embedding → 索引 → 元数据保存
```

这个阶段决定系统能不能找到正确证据。

### 在线问答

```text
用户问题 → 查询改写 → 检索 → 重排 → 上下文组装 → 生成答案 → 引用和评估
```

这个阶段决定系统能不能把证据用好。

## 最小可行版本

最小 RAG 不需要一开始就引入复杂 Agent。可以先做：

1. 收集少量高质量文档。
2. 切成带来源信息的 chunk。
3. 用 [Embedding](embedding.md) 生成向量。
4. 放入 [向量数据库](vector-database.md) 或支持向量检索的搜索系统。
5. 查询时取回 top-k 片段。
6. 把片段和用户问题一起交给 LLM。
7. 要求回答引用来源，并在证据不足时说不知道。

## 关键设计点

- **切块粒度：** 太小会丢上下文，太大召回不准。
- **检索策略：** 只用向量检索容易漏掉关键词、编号和专有名词。
- **重排策略：** 第一轮粗搜后重排，通常比直接取 top-k 更稳。
- **上下文预算：** 不是检索越多越好，噪声会降低回答质量。
- **引用策略：** 答案应能追溯到具体来源或片段。
- **评估策略：** 同时评估检索质量和生成质量。

## 适用范围

适合：

- 设计 RAG 系统整体架构。
- 拆解一个 RAG 问答系统质量差的原因。
- 判断问题出在资料、检索、上下文还是生成阶段。

不适合：

- 把所有 RAG 问题都归因于模型能力。
- 只优化 Prompt，而不检查检索和索引质量。

## 关联页面

- [Retrieval-Augmented Generation](retrieval-augmented-generation.md)
- [Chunking](chunking.md)
- [Embedding](embedding.md)
- [向量数据库](vector-database.md)
- [Hybrid Search](hybrid-search.md)
- [Reranker](reranker.md)
- [RAG 学习地图](../syntheses/rag-learning-map.md)

## 待核实

- 具体 pipeline 名称和模块边界会随框架不同而变化。
