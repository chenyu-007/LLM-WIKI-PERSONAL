---
title: Retrieval-Augmented Generation
type: concept
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-rag-original-paper.source.md
  - raw/sources/2026-05-15-rag-survey.source.md
  - raw/inbox/youdao/approved-2026-05-15/07-retrieval-augmented-generation.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
---

# Retrieval-Augmented Generation

## 一句话说明

Retrieval-Augmented Generation（RAG）是一种先从外部知识源检索相关内容，再让模型基于这些内容生成答案的方法。

## 要点

- RAG 的核心是把模型的参数化知识和外部非参数化知识结合起来。
- RAG 适合需要最新知识、私有知识、来源追溯或领域资料支撑的问答场景。
- RAG 不等于向量数据库。向量库只是常见组件，完整 RAG 还包括切块、索引、检索、重排、上下文组装、生成和评估。
- RAG 可以缓解知识过时和部分幻觉问题，但不能保证完全没有幻觉。
- RAG 的效果通常取决于检索质量、chunk 设计、上下文噪声控制和生成阶段的约束。
- RAG 不是 MCP 的子集。RAG 是一种检索增强生成方法；MCP 是让模型应用连接外部工具、资源和提示的协议。RAG 可以通过 MCP 暴露检索能力，但两者不是包含关系。
- RAG 也不是 LLM Wiki 的替代品。RAG 偏运行时检索和注入上下文，LLM Wiki 偏长期维护一层可读、可校验、可链接的知识。

## 基本流程

```text
资料集合
  ↓
切块和清洗
  ↓
Embedding / 索引
  ↓
用户问题
  ↓
检索和重排
  ↓
组装上下文
  ↓
LLM 生成答案
  ↓
引用和评估
```

## 适用范围

适合：

- 企业知识库问答。
- 个人学习资料检索。
- 技术文档、论文、会议纪要、产品资料问答。
- 需要引用来源的事实型回答。
- 内容经常更新、不适合频繁 fine-tuning 的知识。

不适合：

- 纯创作、风格迁移或格式模仿任务。
- 不需要外部知识的简单推理。
- 源资料质量差、权限边界不清、无法追溯来源的知识库。
- 需要强一致事务或确定性业务逻辑的操作流程。

## 关联页面

- [LLM Wiki](llm-wiki.md)
- [RAG 和 LLM Wiki 怎么配合](../syntheses/rag-vs-llm-wiki.md)
- [RAG 原始论文](../sources/rag-original-paper.md)
- [RAG 大模型综述](../sources/rag-survey.md)
- [RAG Pipeline](rag-pipeline.md)
- [Chunking](chunking.md)
- [Embedding](embedding.md)
- [Hybrid Search](hybrid-search.md)
- [Reranker](reranker.md)
- [为什么 RAG 仍然会幻觉](../questions/why-rag-still-hallucinates.md)
- [RAG 学习地图](../syntheses/rag-learning-map.md)
- [Model Context Protocol](model-context-protocol.md)

## 待核实

- 不同框架会使用不同术语描述 RAG 模块。接入具体框架时，需要核对该框架的定义。
- 向量数据库、Embedding 模型和 RAG 框架更新很快，选型时需要重新查看官方文档。
