---
title: Agent Memory (长期记忆)
type: concept
status: active
updated: 2026-05-27
sources:
  - wiki/sources/一个公式讲清Agent长期记忆AI的记笔记比你想象聪明 先看清问题的本质Agent 的长期记忆不是数据库存的是值得记住的.md
  - wiki/sources/给-Agent-加记忆前-先想清楚这四个问题-研究了一圈-Agent-Memory-框架后的心得选框架之前先搞清楚记给谁记什么记多久怎么取大部分场景其.md
  - wiki/sources/OpenClaw多Agent共用记忆这个方法太香了-OpenClaw-AI助手-Agent-多Agent-人工智能.md
---

# Agent Memory (长期记忆)

## 是什么

Agent 的长期记忆不是数据库——**不是把对话全存下来，而是判断"什么值得记住"**。

## 核心公式

```
记忆价值 = 重要性 × 时效性 × 相关性
```

- **重要性**：这条信息对后续任务有多关键？
- **时效性**：会不会过时？（昨天的 API 文档 vs 上周的 bug fix）
- **相关性**：和当前任务/领域有没有关系？

低于阈值 → 丢弃。高于阈值 → 压缩存储（不是存原文，是存结构化摘要）。

## 加记忆前四个问题

1. **记给谁？** — 单用户还是多用户共享？多 Agent 还是单 Agent？
2. **记什么？** — 用户偏好？任务上下文？领域知识？
3. **记多久？** — 会话级？项目级？永久？
4. **怎么取？** — 关键词检索？语义检索？时间衰减？

大部分场景其实不需要复杂的记忆框架——先想清楚这四个问题，再说要不要上 Mem0 / LangChain Memory / Pinecone。

## 工具

| 工具 | 特点 |
|------|------|
| Mem0 | 轻量级长期记忆，自动过滤噪声 |
| Pinecone Nexus | 编译期知识层，不用每次检索 |
| LangChain Memory | 框架内置，多种记忆类型 |

## 相关页面

- [AI Agent](ai-agent.md)
- [上下文工程](context-engineering.md)
- [Mem0](../entities/mem0.md)
- [Pinecone](../entities/pinecone.md)
