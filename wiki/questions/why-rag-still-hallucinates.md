---
title: 为什么 RAG 仍然会幻觉
type: question
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-rag-survey.source.md
  - raw/sources/2026-05-15-self-rag.source.md
---

# 为什么 RAG 仍然会幻觉

## 一句话说明

RAG 能减少部分幻觉，但如果检索、上下文或生成阶段出错，模型仍然可能生成没有来源支持的答案。

## 要点

- RAG 的回答质量先受检索质量限制：没找对资料，模型就没有正确依据。
- 检索到错误或噪声资料时，模型可能把噪声当成事实。
- 检索到了正确资料，但上下文太长、冲突太多或排序太差，模型也可能忽略关键证据。
- Prompt 没有强制引用和证据约束时，模型可能混用参数知识和检索内容。
- Self-RAG 这类方法试图让模型判断是否需要检索、检索是否相关、回答是否被证据支持。

## 常见原因

| 问题位置 | 典型原因 | 改进方向 |
|---|---|---|
| 资料层 | 原文错误、过期、重复、缺来源 | 清洗资料，保留元数据 |
| 切块层 | chunk 太小或太大 | 按结构切块，保留上下文 |
| 检索层 | 召回错、漏召回 | Hybrid Search，查询改写 |
| 排序层 | 关键证据排在后面 | 使用 Reranker |
| 上下文层 | 塞入太多噪声 | 压缩上下文，限制 top-n |
| 生成层 | 模型自由发挥 | 要求引用来源，只基于证据回答 |

## 判断方法

调试 RAG 幻觉时，不要只看最终答案。应该依次检查：

1. 是否有正确资料进入语料库。
2. 正确资料是否被切成可检索 chunk。
3. 用户问题是否检索到正确 chunk。
4. 正确 chunk 是否排在上下文前部。
5. 模型答案是否能逐句对应到来源。

## 关联页面

- [Retrieval-Augmented Generation](../concepts/retrieval-augmented-generation.md)
- [RAG Pipeline](../concepts/rag-pipeline.md)
- [Chunking](../concepts/chunking.md)
- [Embedding](../concepts/embedding.md)
- [Hybrid Search](../concepts/hybrid-search.md)
- [Reranker](../concepts/reranker.md)
- [RAG 大模型综述](../sources/rag-survey.md)
- [Self-RAG](../sources/self-rag.md)
- [RAG 学习地图](../syntheses/rag-learning-map.md)

## 待核实

- 不同评估框架对 hallucination、faithfulness、groundedness 的定义不同，需要按评估工具确认术语。
