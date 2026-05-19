---
title: MCP 和 RAG 的区别是什么
type: question
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-mcp-official-intro.source.md
  - raw/sources/2026-05-15-mcp-official-architecture.source.md
  - raw/sources/2026-05-15-mcp-official-server-concepts.source.md
  - raw/sources/2026-05-15-rag-original-paper.source.md
---

# MCP 和 RAG 的区别是什么

## 一句话说明

RAG 主要解决模型如何利用检索到的外部知识生成答案，MCP 主要解决 AI 应用如何用标准协议连接外部工具、数据源和工作流。

## 要点

- RAG 的重点是「检索 + 生成」：先从外部知识库检索相关内容，再让模型基于这些内容回答。
- MCP 的重点是「连接协议」：让 AI 应用用统一方式发现、读取和调用外部系统能力。
- RAG 通常围绕知识获取和答案生成；MCP 同时覆盖只读上下文、可调用工具和可复用工作流。
- MCP 可以服务 RAG。例如，MCP Resource 可以暴露知识库页面，MCP Tool 可以执行搜索，AI 应用再把检索结果用于生成。
- MCP 不替代 RAG。它提供连接层和能力边界，RAG 是一种使用外部知识增强生成的技术模式。

## 对比

| 维度 | RAG | MCP |
|---|---|---|
| 核心问题 | 如何让模型利用外部知识回答 | 如何让 AI 应用连接外部系统 |
| 主要对象 | 检索器、知识库、生成模型 | Host、Client、Server、Tools、Resources、Prompts |
| 典型输出 | 带外部依据的回答 | 可被 AI 应用读取或调用的外部能力 |
| 是否执行动作 | 通常不强调执行动作 | 可以通过 Tools 执行动作 |
| 是否是协议 | 不是统一连接协议 | 是开放协议 |

## 什么时候用 RAG

- 目标是基于文档、知识库或网页资料回答问题。
- 主要任务是减少幻觉、提供来源、更新知识。
- 外部系统只需要被读取，不需要复杂操作。

## 什么时候用 MCP

- 目标是把一个外部系统接入 AI 应用。
- 需要同时提供资料读取、工具调用和流程模板。
- 希望同一个能力可以被不同 MCP Host 复用。
- 需要明确权限、连接生命周期、transport 和工具 schema。

## 关联页面

- [Model Context Protocol](../concepts/model-context-protocol.md)
- [MCP Tools、Resources 和 Prompts](../concepts/mcp-tools-resources-prompts.md)
- [Retrieval-Augmented Generation](../concepts/retrieval-augmented-generation.md)
- [RAG 学习地图](../syntheses/rag-learning-map.md)
- [MCP 学习地图](../syntheses/mcp-learning-map.md)
- [MCP 官方介绍](../sources/mcp-official-intro.md)
- [MCP 官方架构说明](../sources/mcp-official-architecture.md)
- [MCP 官方 Server Concepts](../sources/mcp-official-server-concepts.md)
- [RAG 原始论文](../sources/rag-original-paper.md)

## 待核实

- 不同厂商会把 RAG、工具调用和 Agent 编排封装成不同产品形态。比较具体产品时，需要回到对应厂商文档核对边界。
