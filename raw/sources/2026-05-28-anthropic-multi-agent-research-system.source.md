---
title: How we built our multi-agent research system
type: source
status: active
source_url: https://www.anthropic.com/engineering/multi-agent-research-system
author: Anthropic
published: 2025-06-13
captured: 2026-05-28
---

# How we built our multi-agent research system

## 来源说明

这是 Anthropic 官方关于 Claude Research 多 Agent 系统的工程复盘，讨论多 Agent 何时有价值，以及生产系统会遇到的协调、评估和可靠性问题。

## 本 Wiki 中的用途

- 用于校验多 Agent 并不是默认答案，而是适合开放式、广度优先、需要并行探索的研究任务。
- 用于支撑 orchestrator-worker、subagent 并行、结果压缩、可观测性和部署策略等概念。
- 用于回答“什么时候该用多 Agent，什么时候该保持单 Agent”的问题。

## 下游页面

- `wiki/concepts/ai-agent.md`
- `wiki/concepts/context-engineering.md`
- `wiki/syntheses/anthropic-agent-engineering-map.md`
