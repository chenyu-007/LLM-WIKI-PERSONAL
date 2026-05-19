---
title: Karpathy LLM Wiki gist
type: source
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-04-04-karpathy-llm-wiki.source.md
---

# Karpathy LLM Wiki gist

## 来源

- 作者：Andrej Karpathy
- 发布时间：2026-04-04
- URL：https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
- 本地来源记录：`raw/sources/2026-04-04-karpathy-llm-wiki.source.md`

## 核心主张

Karpathy 的原始模式强调：不要只把资料留在原始状态，也不要只做一次性问答。更好的方式是用 LLM 把资料逐步编译成 Markdown Wiki，让知识层可以被人和 AI 共同维护。

## 本地实现取舍

本 Wiki 采用以下部分：

- 使用 `raw/` 存放来源。
- 使用 `wiki/` 存放整理后的知识页。
- 使用 `index.md` 作为主要导航。
- 使用 `log.md` 记录维护行为。
- 使用 `AGENTS.md` 约束 AI 代理。
- 暂不引入复杂脚本、向量库或 MCP。

## 为什么暂不自动化

自动化只有在页面数量和维护成本上来之后才有价值。当前阶段更重要的是把知识粒度、来源引用、页面命名和维护习惯跑顺。

## 可转化页面

- [LLM Wiki](../concepts/llm-wiki.md)
- [RAG 学习地图](../syntheses/rag-learning-map.md)
- [MCP 学习地图](../syntheses/mcp-learning-map.md)

## 待核实

- 如果后续引用 gist 中更细的实现细节，需要回到原文逐条核对。
