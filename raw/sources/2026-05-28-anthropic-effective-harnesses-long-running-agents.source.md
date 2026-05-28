---
title: Effective harnesses for long-running agents
type: source
status: active
source_url: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
author: Anthropic
published: 2025-11-26
captured: 2026-05-28
---

# Effective harnesses for long-running agents

## 来源说明

这是 Anthropic 官方关于长时间运行 Agent harness 的文章，关注 Agent 如何跨多个上下文窗口持续推进复杂任务。

## 本 Wiki 中的用途

- 用于支撑本地 LLM Wiki 的维护闭环：长任务必须留下可接力的工件，而不是依赖上一轮对话记忆。
- 用于校验 initializer agent、coding agent、incremental progress、handoff artifacts 等长任务设计思想。
- 用于后续设计 Codex/Hermes 共享 LLM Wiki 时作为长任务接力参考。

## 下游页面

- `wiki/concepts/context-engineering.md`
- `wiki/concepts/agent-memory.md`
- `wiki/syntheses/anthropic-agent-engineering-map.md`
