---
title: PRD 还是原型？AI 开发时代的需求表达方式
type: question
status: active
updated: 2026-05-27
sources:
  - wiki/sources/Cat-WuPRD已死原型万岁-Anthropic产品经理的新工作流-辉子分享让AI根据PRD开发功能却总是差点意思的尴.md
---

# PRD 还是原型？AI 开发时代的需求表达方式

## 问题

给 AI 写 PRD（产品需求文档）开发功能，总是"差点意思"——写再多文字，AI 理解出来的东西和你想要的之间总有偏差。怎么办？

## 回答：原型代替 PRD

Anthropic 产品经理 Cat Wu 的实践：

1. **PRD 的问题**：文字描述存在歧义，AI 从文字推断意图的链路太长。
2. **原型的优势**：做一个可交互的原型给 AI 看，比一千行文字更精准。
3. **效果**：AI 根据原型直接生成功能代码，偏差大幅缩小。

## 适用场景

| 场景 | 推荐 |
|------|------|
| 简单功能（加个按钮/改样式） | PRD 足够 |
| 复杂交互（多步骤流程/新页面） | 原型 > PRD |
| 探索性功能（不确定怎么做） | 先做原型验证，再让 AI 实现 |

## 相关页面

- [AI 工作流](../concepts/ai-workflow.md)
- [Anthropic](../entities/anthropic.md)
