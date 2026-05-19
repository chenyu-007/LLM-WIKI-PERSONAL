---
title: RAG 和 Fine-tuning 怎么选
type: question
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-rag-original-paper.source.md
  - raw/sources/2026-05-15-aws-rag-vs-fine-tuning.source.md
---

# RAG 和 Fine-tuning 怎么选

## 一句话说明

RAG 更适合接入会变化、需要引用的外部知识；Fine-tuning 更适合调整模型稳定行为、格式、风格或领域任务表现。

## 要点

- RAG 不改变模型参数，而是在回答时检索外部资料。
- Fine-tuning 会调整模型参数，让模型更符合目标任务或输出风格。
- 如果知识经常变化，优先考虑 RAG。
- 如果目标是稳定输出格式、语气、分类规则或特定任务行为，优先考虑 Fine-tuning。
- 二者可以组合：Fine-tuning 负责行为模式，RAG 负责外部知识。

## 决策表

| 目标 | 更适合 |
|---|---|
| 使用最新文档回答问题 | RAG |
| 引用来源、可追溯 | RAG |
| 接入企业或个人私有知识库 | RAG |
| 模仿固定格式或语气 | Fine-tuning |
| 提高特定分类或抽取任务表现 | Fine-tuning |
| 降低长期 prompt 复杂度 | Fine-tuning |
| 同时需要知识更新和稳定行为 | RAG + Fine-tuning |

## 常见误区

- 误区：Fine-tuning 可以把所有知识塞进模型。
- 现实：知识会过期，也难以追溯来源。频繁变化的知识更适合 RAG。
- 误区：RAG 可以替代所有模型训练。
- 现实：RAG 解决知识接入，不直接解决模型风格、格式和任务行为的一致性。

## 适用范围

适合：

- 做技术选型。
- 判断知识库问答、客服、文档助手该用哪种方案。
- 解释为什么很多系统会把 RAG 和 Fine-tuning 组合使用。

不适合：

- 不看数据质量就决定方案。
- 把成本、延迟、安全和维护全部忽略，只比较概念。

## 关联页面

- [Retrieval-Augmented Generation](../concepts/retrieval-augmented-generation.md)
- [RAG 原始论文](../sources/rag-original-paper.md)
- [AWS RAG vs Fine-tuning 对比](../sources/aws-rag-vs-fine-tuning.md)
- [RAG 学习地图](../syntheses/rag-learning-map.md)

## 待核实

- 具体模型供应商的 fine-tuning 能力、价格和限制会变化，落地时需要查最新官方文档。
