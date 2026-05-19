---
title: Tavily Docs
type: source
status: active
updated: 2026-05-16
sources:
  - raw/sources/2026-05-16-tavily-docs.source.md
---

# Tavily Docs

## 来源

- 作者：Tavily
- 发布时间：未标明
- URL：https://docs.tavily.com/
- 本地来源记录：`raw/sources/2026-05-16-tavily-docs.source.md`

## 核心内容

- Tavily 官方文档把 Tavily 定位为面向开发者的 Web search、extract、crawl、map 和 research API。
- Tavily API 的基础地址是 `https://api.tavily.com`，通过 API key 鉴权。
- 核心端点包括 `/search`、`/extract`、`/crawl`、`/map` 和 `/research`。
- Tavily Search 可以返回结构化搜索结果，结果中包含标题、URL、内容片段、相关度分数等字段，也可以按参数返回 LLM 生成的答案、原始内容或图片信息。
- Tavily 提供 Python SDK、JavaScript SDK 和 MCP Server 文档，说明它常用于 AI Agent 和 RAG 的外部搜索能力。

## 可转化页面

- 实体：[Tavily](../entities/tavily.md)
- 问题：[Tavily 和 Browserbase 怎么区分](../questions/tavily-vs-browserbase.md)

## 待核实

- Tavily 的端点、价格、额度和 SDK 版本会变化，接入前需要重新查看官方文档。
