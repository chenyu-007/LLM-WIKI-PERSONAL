---
title: Tavily
type: entity
status: active
updated: 2026-05-16
sources:
  - raw/sources/2026-05-16-tavily-docs.source.md
---

# Tavily

## 基本信息

- 类型：AI Search API / Web content API
- 所属领域：AI Agent、RAG、联网搜索、网页内容获取
- 关键时间：官方文档捕获于 2026-05-16

## 与本 Wiki 的关系

Tavily 是 AI Agent 和 RAG 系统常见的外部搜索工具。它适合为模型提供实时网页搜索、网页内容抽取、站点爬取、站点地图和深度研究能力。

## 关联事实

- Tavily 的核心端点包括 `/search`、`/extract`、`/crawl`、`/map` 和 `/research`。
- Tavily Search 返回结构化搜索结果，适合被 LLM 或 Agent 继续消费。
- Tavily 可以作为 RAG 的网页检索来源，也可以作为 MCP Tool 接入 AI 应用。
- Tavily 更适合「查找和获取网页信息」，不适合替代真实浏览器交互。

## 适用范围

适合：

- 查询最新网页资料。
- 给 RAG 系统补充 Web 检索来源。
- 给 Agent 提供联网搜索和网页内容抽取能力。
- 通过 MCP 或 SDK 暴露为可调用工具。

不适合：

- 登录网站、点击按钮、填写表单、下载文件等需要真实浏览器会话的任务。
- 替代人工确认的高风险网页操作。
- 不需要联网的本地知识库检索。

## 关联页面

- [Tavily Docs](../sources/tavily-docs.md)
- [Tavily 和 Browserbase 怎么区分](../questions/tavily-vs-browserbase.md)
- [Retrieval-Augmented Generation](../concepts/retrieval-augmented-generation.md)
- [Model Context Protocol](../concepts/model-context-protocol.md)

## 待核实

- 具体 API 价格、额度、返回字段和 MCP Server 配置需要在使用前重新核对官方文档。
