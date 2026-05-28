---
title: Agent Skill
type: concept
status: active
updated: 2026-05-25
sources:
  - wiki/sources/findskills帮你智能调用合适的skills-你有没有这种情况你现在想解决一个问题但不知道如何在海量的-Skills-里找到刚好能帮到你的那个这个.md
  - wiki/sources/5分钟解锁小龙虾Skill全攻略什么是Skill有哪些好用-skill如何安装小白必看进化指南openclaw-skill-ai-前沿科技趋势.md
  - wiki/sources/Hermes-装上这5个skills-直接起飞-Hermes-科技-ai-模型.md
  - wiki/sources/为什么你的skill没用-大模型应用-AI应用开发-Agent开发-Anthropic.md
---

# Agent Skill

## 是什么

Agent Skill 是一种**可复用的指令模板**，告诉 AI Agent 在特定场景下应该如何行为——类似给 Agent 安装的"技能插件"。

- 每个 Skill 包含触发条件、工作步骤、边界规则。
- 启动时只加载名称和描述（渐进加载），触发时才读取完整指令。
- 遵循 [Agent Skills 规范](https://agentskills.io/specification)：一个 Skill 至少是一个包含 `SKILL.md`（YAML frontmatter + 正文）的目录。

## 为什么需要 Skill

1. **减少重复指令** — 不用每次都写"遇到 bug 先排查再修"。
2. **保证一致性** — 同一类任务每次用同一套规则。
3. **可组合** — 多个 Skill 可以串联成工作流。
4. **可迁移** — Skill 文件可以在不同 AI 客户端间复制。

## Skill vs MCP

| 维度 | Skill | MCP |
|------|-------|-----|
| 本质 | 规则/指令模板（告诉 AI **怎么做**） | 工具接口（给 AI **可调用的能力**） |
| 形式 | Markdown 文件 | 外部服务（stdio/HTTP） |
| 示例 | "写计划前先拆分步骤" | `parse_douyin_video_info` |
| 加载 | 渐进加载，触发时读正文 | 客户端启动时连接 |

**Skill 控制行为，MCP 扩展能力。两者互补：Skill 可以规定"遇到抖音链接优先用 MCP 工具"。**

## 好 Skill 的特征

- 触发条件明确（"遇到 X 时使用"）
- 步骤可执行（不是泛泛的"做好一点"）
- 有边界规则（什么不干、什么时候停）
- 有验证要求（完成前必须检查）

## 相关页面

- [Model Context Protocol](model-context-protocol.md)
- [MCP Tools Resources Prompts](mcp-tools-resources-prompts.md)
- [AI Agent](ai-agent.md)
