---
title: MCP 官方架构说明
type: source
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-mcp-official-architecture.source.md
---

# MCP 官方架构说明

## 来源

- 作者：Model Context Protocol
- 发布时间：未标明
- URL：https://modelcontextprotocol.io/docs/learn/architecture
- 本地来源记录：`raw/sources/2026-05-15-mcp-official-architecture.source.md`

## 核心内容

- MCP 的范围包括协议规范、SDK、开发工具和参考服务器实现。
- MCP 采用 Host、Client、Server 的参与者模型：Host 是 AI 应用，Client 维护到某个 Server 的连接，Server 向 Client 提供上下文能力。
- MCP Server 可以本地运行，也可以远程运行；区别通常体现在 transport 选择和部署位置上。
- MCP 分为 Data Layer 和 Transport Layer。Data Layer 处理 JSON-RPC 语义、生命周期、能力协商和 primitives；Transport Layer 处理通信通道、消息传输和认证。
- MCP 关注上下文交换协议本身，不直接规定 AI 应用如何调用 LLM 或管理内部上下文。

## 可转化页面

- 概念：[Model Context Protocol](../concepts/model-context-protocol.md)
- 概念：[MCP Tools、Resources 和 Prompts](../concepts/mcp-tools-resources-prompts.md)
- 综合：[MCP 学习地图](../syntheses/mcp-learning-map.md)

## 待核实

- 官方文档会随协议修订更新；涉及 transport、协议版本或鉴权细节时需要回到最新规范复核。
