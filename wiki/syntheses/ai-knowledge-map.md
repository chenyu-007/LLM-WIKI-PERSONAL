---
title: AI 知识库全景图
type: synthesis
status: active
updated: 2026-05-25
sources:
  - wiki/sources/跟Karpathy学搭建AI知识库-Obsidian实践-KarpathyOpenAI创始人之一特斯拉前AI总监最近发了个LLM-Wiki框架3天500.md
  - wiki/sources/为什么Obsidian是AI时代最佳知识管理工具-用了18年笔记软件从Evernote到Notion从Roam到logseq最终我选择了Obsidian.md
  - wiki/sources/笔记本会自我进化-拥有一个会自我进化的笔记本知识科普-知识分享-AI-AI知识库-笔记.md
  - wiki/sources/工具已开源我的优化版-Karpathy知识库-折腾了好几天终于搞完开源了.md
  - ../wiki/concepts/llm-wiki.md
---

# AI 知识库全景图

## 核心理念

来自 Karpathy 的 LLM Wiki 框架：**不要把资料留在原始状态，用 LLM 逐步编译成可维护的 Markdown Wiki。**

这不是一个新技术，而是一套**理念和行为准则**——没有技术门槛，每个人都可以借鉴。

## 架构层次

```
raw/          原始资料（转录、截图、来源记录）
    ↓ 消化
wiki/
  sources/    来源摘要（这个资料说了什么）
  concepts/   概念解释（这个术语是什么意思）
  entities/   实体记录（这个工具/人物/项目是什么）
  questions/  问题解答（这个反复出现的问题怎么判断）
  syntheses/  综合（多个来源合起来说明了什么）
```

## 为什么 Obsidian

- 本地 Markdown 文件，完全受控。
- 双向链接（`[[wiki/concepts/xxx]]`）。
- 不依赖云服务，AI 可以直接读写。
- 18 年笔记软件经验验证的最佳选择。

## 关键原则

1. **来源可追溯** — 每个结论都指向 `raw/`。
2. **渐进消化** — raw → source → concept/entity → synthesis。
3. **一个页面一个主题** — 不堆砌。
4. **先跑通手工流程** — 自动化在维护成本上来之后才有价值。
5. **AI 和人共同维护** — `AGENTS.md` 约束 AI，`log.md` 记录变更。

## 相关页面

- [LLM Wiki](../concepts/llm-wiki.md)
- [Agent Skill](../concepts/agent-skill.md)
- [OpenClaw](../entities/openclaw.md)
- [Claude Code](../entities/claude-code.md)
