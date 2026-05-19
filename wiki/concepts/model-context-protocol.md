---
title: Model Context Protocol
type: concept
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-mcp-official-intro.source.md
  - raw/sources/2026-05-15-mcp-official-architecture.source.md
  - raw/sources/2026-05-15-mcp-official-server-concepts.source.md
---

# Model Context Protocol

## 一句话说明

Model Context Protocol（MCP）是连接 AI 应用与外部工具、数据源和工作流的开放协议。

## 要点

- MCP 不是模型，也不是 Agent 框架；它解决的是 AI 应用和外部系统之间的标准连接问题。
- MCP 的核心参与者是 Host、Client 和 Server。Host 是 AI 应用，Client 负责维护到某个 Server 的连接，Server 负责暴露上下文和能力。
- MCP Server 可以暴露 Tools、Resources 和 Prompts。三者分别对应执行动作、读取上下文和复用工作流。
- MCP 采用分层设计：Data Layer 负责协议语义和 primitives，Transport Layer 负责通信通道、消息传输和认证。
- MCP 关注上下文交换协议，不规定 AI 应用内部如何调用模型、裁剪上下文或执行推理策略。

## 核心结构

```text
AI 应用 / MCP Host
  ↓
MCP Client
  ↓
MCP Server
  ↓
外部系统：文件、数据库、API、业务工具、知识库
```

一个 Host 可以连接多个 MCP Server。通常每个 MCP Client 维护到一个 MCP Server 的一对一连接。

## 适用范围

适合：

- 让 AI 应用访问本地文件、数据库、API、企业系统或个人知识库。
- 把已有系统包装成 AI 可发现、可调用、可授权的能力。
- 在多个 AI 客户端之间复用同一套外部工具接口。
- 为 Agent 提供稳定的工具、资源和工作流边界。

不适合：

- 只需要一次性问答、没有外部系统接入的场景。
- 需要模型内部推理能力提升的问题。
- 没有权限边界、审计或确认机制的高风险写操作。

## 关联页面

- [LLM Wiki](llm-wiki.md)
- [MCP 官方介绍](../sources/mcp-official-intro.md)
- [MCP 官方架构说明](../sources/mcp-official-architecture.md)
- [MCP Tools、Resources 和 Prompts](mcp-tools-resources-prompts.md)
- [MCP 和 RAG 的区别是什么](../questions/mcp-vs-rag.md)
- [MCP 学习地图](../syntheses/mcp-learning-map.md)

## 待核实

- MCP 规范仍在迭代。涉及协议版本、transport、安全策略和客户端兼容性时，需要回到官方 specification 核对。
