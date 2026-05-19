---
title: Browserbase
type: entity
status: active
updated: 2026-05-16
sources:
  - raw/sources/2026-05-16-browserbase-docs.source.md
---

# Browserbase

## 基本信息

- 类型：AI Browser Automation Platform / Cloud Browser Infrastructure
- 所属领域：AI Agent、浏览器自动化、网页交互、数据获取
- 关键时间：官方文档捕获于 2026-05-16

## 与本 Wiki 的关系

Browserbase 是 AI Agent 访问和操作真实网页时常见的基础设施。它适合提供隔离浏览器会话、网页搜索、页面抓取、函数部署、模型访问、Agent Identity 和可观测性。

## 关联事实

- Browserbase 的核心定位是构建和部署能像人一样浏览、交互网页的 Agent。
- Browserbase 提供 headless browsers、search、fetch、functions、model gateway、identity 和 observability。
- Browserbase 适合处理登录、JavaScript 渲染、交互流程、表单、截图和浏览器自动化任务。
- Stagehand 是 Browserbase 生态中的 AI-native browser automation SDK，提供 `act`、`extract`、`observe` 和 `agent` 等原语。
- Browserbase 更适合「真实网页交互」，不适合替代轻量搜索 API。

## 适用范围

适合：

- 网站没有稳定 API，只能通过网页操作完成任务。
- 需要真实浏览器、登录态、Cookie、截图或文件下载。
- 需要用 Playwright、Puppeteer、Selenium 或 Stagehand 做浏览器自动化。
- 需要为 Agent 提供隔离、可观测的云端浏览器环境。

不适合：

- 只是查资料或抓取公开网页摘要。
- 已有稳定 API 可以直接调用的业务系统。
- 不需要浏览器渲染的本地文档检索。
- 未经人工确认的高风险账号操作。

## 关联页面

- [Browserbase Docs](../sources/browserbase-docs.md)
- [Tavily 和 Browserbase 怎么区分](../questions/tavily-vs-browserbase.md)
- [Model Context Protocol](../concepts/model-context-protocol.md)

## 待核实

- Browserbase 的 Identity、Model Gateway、Functions 和 Stagehand 能力仍可能快速变化，具体接入前需要查最新文档。
