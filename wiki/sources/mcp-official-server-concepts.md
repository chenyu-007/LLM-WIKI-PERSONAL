---
title: MCP 官方 Server Concepts
type: source
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-mcp-official-server-concepts.source.md
---

# MCP 官方 Server Concepts

## 来源

- 作者：Model Context Protocol
- 发布时间：未标明
- URL：https://modelcontextprotocol.io/docs/learn/server-concepts
- 本地来源记录：`raw/sources/2026-05-15-mcp-official-server-concepts.source.md`

## 核心内容

- MCP Server 是通过标准协议接口向 AI 应用暴露能力的程序。
- 官方把 server features 归纳为三类 building blocks：Tools、Resources、Prompts。
- Tools 是模型可主动调用的操作接口，通常带有结构化输入输出，也可能产生副作用。
- Resources 是应用可读取并提供给模型的上下文数据，通常以 URI 或 URI 模板定位。
- Prompts 是面向用户显式选择的可复用提示词模板，用于把常见任务固化成结构化工作流。
- 多个 MCP Server 可以被同一个 AI 应用组合使用，形成统一的外部能力接口。

## 可转化页面

- 概念：[MCP Tools、Resources 和 Prompts](../concepts/mcp-tools-resources-prompts.md)
- 问题：[MCP 和 RAG 的区别是什么](../questions/mcp-vs-rag.md)
- 综合：[MCP 学习地图](../syntheses/mcp-learning-map.md)

## 待核实

- 具体协议方法、参数 schema 和权限模型应在实现时回到 MCP specification 或对应 SDK 文档核对。
