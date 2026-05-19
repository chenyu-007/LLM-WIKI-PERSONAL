---
title: MCP Tools、Resources 和 Prompts
type: concept
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-mcp-official-architecture.source.md
  - raw/sources/2026-05-15-mcp-official-server-concepts.source.md
---

# MCP Tools、Resources 和 Prompts

## 一句话说明

Tools、Resources 和 Prompts 是 MCP Server 向 AI 应用暴露能力的三类核心 building blocks。

## 要点

- **Tools：** 模型可主动请求调用的操作接口，适合搜索、创建、修改、发送消息、调用外部 API 等动作。
- **Resources：** 应用可读取并注入上下文的数据源，适合文件、数据库 schema、API 文档、知识库页面等只读信息。
- **Prompts：** 用户可显式选择的提示词模板，适合把常见任务封装成稳定工作流。
- 官方文档把三者的控制主体区分开：Tools 主要由模型决定是否调用，Resources 主要由应用决定如何纳入上下文，Prompts 主要由用户显式选择。
- 三者可以组合使用：Prompt 固定任务入口，Resource 提供背景资料，Tool 执行外部动作。

## 选择原则

```text
要执行动作 → Tool
要读取上下文 → Resource
要复用交互流程 → Prompt
```

## 典型例子

| 类型 | 适合内容 | 不适合内容 |
|---|---|---|
| Tool | 搜索文件、创建 Issue、查询数据库、发送消息 | 静态文档全文、纯说明性资料 |
| Resource | 文件内容、知识库页面、数据库 schema、API 参考 | 有副作用的写操作 |
| Prompt | 总结会议、生成周报、规划旅行、整理来源 | 需要自动触发的隐藏逻辑 |

## 用在个人知识库时

如果给本地 `llm-wiki` 设计 MCP 接入，可以先这样划分：

- `wiki://index`、`wiki://concepts/{slug}` 适合做 Resources。
- `search_wiki`、`ingest_source` 适合做 Tools。
- `create_concept_page`、`summarize_source` 适合做 Prompts。

这是本地适配建议，不是官方强制结构。

## 适用范围

适合：

- 设计 MCP Server 的能力边界。
- 判断一个外部能力应该暴露为可调用动作、只读资料还是交互模板。
- 为 Agent 工具调用设置权限和确认边界。

不适合：

- 直接替代底层业务 API 设计。
- 把所有能力都包装成 Tool，导致模型误调用高风险操作。
- 把需要用户明确选择的流程隐藏成自动行为。

## 关联页面

- [Model Context Protocol](model-context-protocol.md)
- [MCP 官方 Server Concepts](../sources/mcp-official-server-concepts.md)
- [MCP 学习地图](../syntheses/mcp-learning-map.md)

## 待核实

- 实现 MCP Server 时，需要继续核对对应 SDK 的 schema 写法、错误返回格式和权限确认机制。
