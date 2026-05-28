---
title: Code execution with MCP: Building more efficient agents
type: source
status: active
source_url: https://www.anthropic.com/engineering/code-execution-with-mcp
author: Anthropic
published: 2025-11-04
captured: 2026-05-28
---

# Code execution with MCP: Building more efficient agents

## 来源说明

这是 Anthropic 官方关于 MCP 与代码执行结合的文章，讨论当 Agent 接入大量工具时，如何避免工具定义和中间结果过度消耗上下文。

## 本 Wiki 中的用途

- 用于校验“不要把所有工具定义一次性塞进上下文”的工程原则。
- 用于支撑把 MCP server 暴露成可按需读取的代码 API、文件树或搜索入口。
- 用于补充 `MCP Tools, Resources, and Prompts` 与 `Agent Skill vs MCP` 的实践边界。

## 下游页面

- `wiki/concepts/model-context-protocol.md`
- `wiki/concepts/mcp-tools-resources-prompts.md`
- `wiki/questions/agent-skill-vs-mcp.md`
- `wiki/syntheses/anthropic-agent-engineering-map.md`
