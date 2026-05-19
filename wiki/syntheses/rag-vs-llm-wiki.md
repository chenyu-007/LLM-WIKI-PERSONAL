---
title: RAG 和 LLM Wiki 怎么配合
type: synthesis
status: active
updated: 2026-05-16
sources:
  - raw/sources/2026-05-15-rag-original-paper.source.md
  - raw/sources/2026-04-04-karpathy-llm-wiki.source.md
  - raw/inbox/youdao/approved-2026-05-15/07-retrieval-augmented-generation.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
---

# RAG 和 LLM Wiki 怎么配合

## 一句话说明

RAG 负责在回答时检索外部材料，LLM Wiki 负责把长期有价值的材料整理成可维护、可链接、可审计的知识层。

## 核心区别

- RAG 的重点是运行时：用户提问后，系统检索相关片段，把片段放进上下文，再让模型回答。
- LLM Wiki 的重点是维护时：把来源、概念、问题和综合结论整理成 Markdown 页面，让人和 AI 都能反复阅读。
- RAG 可以直接检索原始文档，但原始文档噪声通常更高。
- LLM Wiki 可以作为 RAG 的高信噪比语料层，让检索结果更短、更准、更容易引用。

## 推荐组合

```text
raw/ 原始资料
  ↓ 人和 AI 审核
wiki/ 结构化 Markdown 知识层
  ↓ 全文搜索或向量检索
RAG 上下文
  ↓
LLM 回答并引用来源
```

## 什么时候只用 LLM Wiki

- 页面数量少，AI 可以直接读 `index.md` 和相关页面。
- 问题集中在已有概念、学习地图、FAQ 和维护规则。
- 更看重来源可追溯、人工审核和长期演化，而不是大规模自动召回。

## 什么时候加入 RAG

- 页面和原始资料多到人工导航变慢。
- 查询经常跨多个目录、多个主题或多个来源。
- 需要在回答时动态召回大量页面片段。
- 需要把 `raw/` 和 `wiki/` 同时纳入搜索，但仍要区分已审核知识和原始资料。

## 对当前知识库的做法

- 现阶段先维护好 [LLM Wiki](../concepts/llm-wiki.md)、[RAG 学习地图](rag-learning-map.md) 和主题页面。
- 当 `wiki/` 页面继续增长后，先接入全文搜索。
- 当全文搜索不够时，再引入 [Retrieval-Augmented Generation](../concepts/retrieval-augmented-generation.md) 和 [Embedding](../concepts/embedding.md)。
- 如果要让外部 AI 稳定访问，可以通过 [Model Context Protocol](../concepts/model-context-protocol.md) 暴露只读资源或搜索工具。

## 关联页面

- [LLM Wiki](../concepts/llm-wiki.md)
- [Retrieval-Augmented Generation](../concepts/retrieval-augmented-generation.md)
- [RAG Pipeline](../concepts/rag-pipeline.md)
- [Model Context Protocol](../concepts/model-context-protocol.md)

## 待核实

- 具体 RAG 检索实现、Embedding 模型和向量数据库选型需要到实现阶段再按最新官方文档确认。
