---
title: Reranker
type: concept
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-rag-survey.source.md
---

# Reranker

## 一句话说明

Reranker 是在初步检索后重新排序候选片段的模型或模块，用于把最相关的证据排到前面。

## 要点

- Retriever 负责粗召回，Reranker 负责精排。
- 常见做法是先检索较多候选，再让 Reranker 评估 query 和每个候选片段的相关性。
- Reranker 通常比第一阶段检索更慢、更贵，但能提升上下文质量。
- Reranker 特别适合 top-k 检索结果噪声多、相似片段多、答案埋在候选列表后面的场景。

## 工作位置

```text
用户问题
  ↓
Retriever 粗召回
  ↓
Reranker 精排
  ↓
选择 top-n 片段
  ↓
组装上下文并生成答案
```

## 适用范围

适合：

- 候选片段很多，但上下文窗口有限。
- 向量检索能召回相关资料，但排序不稳定。
- 需要提高引用准确性和答案支撑度。

不适合：

- 文档很少，根本不需要复杂排序。
- 延迟和成本极敏感，无法接受额外模型调用。
- 没有评估方法，无法判断重排是否改善结果。

## 关联页面

- [RAG Pipeline](rag-pipeline.md)
- [Hybrid Search](hybrid-search.md)
- [Embedding](embedding.md)
- [为什么 RAG 仍然会幻觉](../questions/why-rag-still-hallucinates.md)

## 待核实

- Reranker 模型选择和 top-k 参数需要通过实际查询集评估。
