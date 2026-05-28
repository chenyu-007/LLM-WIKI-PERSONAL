---
title: AI 工作流
type: concept
status: seed
updated: 2026-05-27
sources:
  - wiki/sources/为什么AI越强你越需要亲手设计工作流-这两天看了Anthropic的一篇文章Building-effective-agents.md
  - wiki/sources/Cat-WuPRD已死原型万岁-Anthropic产品经理的新工作流-辉子分享让AI根据PRD开发功能却总是差点意思的尴.md
---

# AI 工作流

## 核心理念

**AI 越强，你越需要亲手设计工作流。** Anthropic 的观点：不是让 AI 替代你的思考，而是把你自己验证过的流程，拆成 AI 能执行的步骤。

## 为什么 PRD 不行

Anthropic 产品经理 Cat Wu 的实践：

- PRD（产品需求文档）写再多字，AI 理解出来总是"差点意思"。
- **原型代替 PRD** — 做一个可交互的原型给 AI 看，比一千行文字更精准。
- AI 根据原型直接生成功能代码，偏差大幅缩小。

## 设计原则

1. **先跑通手工流程** — 你自己都不知道怎么做，AI 更不行。
2. **拆成小步骤** — 每步可验证、可回滚。
3. **用工件代替口述** — 原型、Skill 文件、检查清单，比聊天记录可靠。
4. **自动化在后** — 流程跑顺手了再写脚本，不要在探索阶段过早自动化。

## 相关页面

- [AI Agent](ai-agent.md)
- [Agent Skill](agent-skill.md)
- [上下文工程](context-engineering.md)
