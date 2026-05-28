---
title: 上下文工程
type: concept
status: seed
updated: 2026-05-27
sources:
  - wiki/sources/Claude-Code上下文工程详解-ai-技术分享-Agent.md
  - wiki/sources/上下文腐烂-Context-rot-其实是两种病-大家都在抱怨-agent-越改越烂开一个新对话就一次改对了-这件事过去半年被反复说叫-conte.md
---

# 上下文工程

## 是什么

上下文工程是**管理 AI Agent 可见信息**的方法论——决定 Agent 在每一步"看到什么"，而非把所有东西塞进 prompt。

## 核心问题：Context Rot（上下文腐烂）

Agent 越改越烂不是因为能力退化，而是上下文在**腐烂**：

1. **膨胀腐烂** — 对话越长，无关信息越多，Agent 被噪音淹没。
2. **漂移腐烂** — 修改过程中旧假设没清理，新老指令互相矛盾。

## 解法

| 问题 | 解法 |
|------|------|
| 膨胀腐烂 | 定期修剪上下文、只保留关键决策 |
| 漂移腐烂 | 每次修改前清理过时指令、重新校准 |
| 根本原因 | 把关键决策写成**可追踪的工件**（Skill 文件、计划文档），而不是只活在聊天记录里 |

## 相关页面

- [AI Agent](ai-agent.md)
- [Agent Memory](agent-memory.md)
- [AI 工作流](ai-workflow.md)
