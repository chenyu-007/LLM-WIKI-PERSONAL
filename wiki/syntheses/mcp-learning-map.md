---
title: MCP 学习地图
type: synthesis
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-mcp-official-intro.source.md
  - raw/sources/2026-05-15-mcp-official-architecture.source.md
  - raw/sources/2026-05-15-mcp-official-server-concepts.source.md
---

# MCP 学习地图

## 一句话说明

学习 MCP 时，先理解它是连接协议，再学习 Host、Client、Server 的架构，最后区分 Tools、Resources 和 Prompts 的能力边界。

## 学习顺序

1. **MCP 的定位：** 先读 [Model Context Protocol](../concepts/model-context-protocol.md)，确认它不是模型，也不是 Agent 框架。
2. **架构角色：** 理解 Host、Client、Server 的连接关系，避免把模型本身和协议参与者混在一起。
3. **能力原语：** 读 [MCP Tools、Resources 和 Prompts](../concepts/mcp-tools-resources-prompts.md)，掌握动作、数据和工作流的边界。
4. **和 RAG 对比：** 读 [MCP 和 RAG 的区别是什么](../questions/mcp-vs-rag.md)，明确 MCP 是连接层，RAG 是知识增强生成模式。
5. **再考虑实现：** 只有当需要把某个系统接入 AI 应用时，再进入 MCP Server 设计和 SDK 实现。

## 关键问题

- MCP Server 到底暴露什么能力？
- 这个能力应该是 Tool、Resource 还是 Prompt？
- 哪些操作有副作用，需要用户确认？
- 哪些数据可以只读暴露，哪些数据需要权限隔离？
- 这个能力是否值得做成 MCP，还是普通脚本、普通 API 或一次性处理就够？

## 对个人知识库的启发

本地 `llm-wiki` 当前阶段不需要立刻实现 MCP Server。更合理的顺序是：

1. 先把 `raw/`、`wiki/`、`index.md` 和 `log.md` 的维护流程跑顺。
2. 当页面数量变多、跨页面检索开始麻烦时，再考虑搜索工具或 MCP Resource。
3. 当需要让外部 AI 应用稳定读取这套知识库时，再考虑设计 MCP Server。
4. 初始 MCP 接入应优先只读 Resource，再逐步增加低风险 Tool。

## 不急着做的事

- 不急着做向量库。
- 不急着做完整知识图谱。
- 不急着把所有文件操作暴露成 Tool。
- 不急着做自动导入，尤其是未经来源核验的外部资料。

## 关联页面

- [LLM Wiki](../concepts/llm-wiki.md)
- [MCP 官方介绍](../sources/mcp-official-intro.md)
- [MCP 官方架构说明](../sources/mcp-official-architecture.md)
- [MCP 官方 Server Concepts](../sources/mcp-official-server-concepts.md)
- [Model Context Protocol](../concepts/model-context-protocol.md)
- [MCP Tools、Resources 和 Prompts](../concepts/mcp-tools-resources-prompts.md)
- [MCP 和 RAG 的区别是什么](../questions/mcp-vs-rag.md)

## 待核实

- 如果后续要写 MCP Server 实现计划，需要单独核对当前 MCP specification、SDK 示例和目标客户端兼容性。
