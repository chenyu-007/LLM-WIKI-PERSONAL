---
title: Claude Code
type: entity
status: active
updated: 2026-05-25
sources:
  - wiki/sources/Claude-Code上下文工程详解-ai-技术分享-Agent.md
  - wiki/sources/这应该是最全面的Claude-Code源码分析了人工智能-互联网大厂-chatgpt应用领域-AI-编程.md
---

# Claude Code

## 是什么

Claude Code 是 Anthropic 推出的 AI 编程助手，在终端中直接运行，可以读写文件、运行命令、使用 Git。

## 关键特性

- **上下文工程** — 通过 `CLAUDE.md` 注入项目级和用户级记忆。
- **Skill 支持** — 可通过 `@path` 导入外部 Markdown 规则文件。
- **终端原生** — 不需要 IDE 插件，直接在命令行使用。
- **源码可分析** — 社区对其架构已有深入分析。

## 与 Reasonix/Codex 的关系

- Claude Code 使用 `CLAUDE.md` 作为记忆文件，类似 Reasonix 的 Skill 系统和 `MEMORY.md`。
- Skill 迁移时可以把 `SKILL.md` 作为 `@import` 规则文档使用。

## 相关页面

- [Agent Skill](../concepts/agent-skill.md)
- [OpenClaw](openclaw.md)
