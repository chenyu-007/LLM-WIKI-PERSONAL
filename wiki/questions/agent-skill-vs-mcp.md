---
title: Agent Skill 和 MCP 最根本的差异
type: question
status: active
updated: 2026-05-25
sources:
  - wiki/sources/面试官问说说-Agent-Skill-和-MCP-最根本的差异.md
  - ../concepts/agent-skill.md
  - ../concepts/model-context-protocol.md
---

# Agent Skill 和 MCP 最根本的差异

## 问题

面试常问：Agent Skill 和 MCP 到底有什么区别？什么时候用哪个？

## 回答

**Skill 是规则，MCP 是工具。**

| | Skill | MCP |
|---|-------|-----|
| **本质** | 指令模板 — 规定 Agent **怎么做** | 协议接口 — 给 Agent **调什么** |
| **形式** | Markdown 文件（`SKILL.md`） | 外部进程或 HTTP 服务 |
| **触发** | AI 根据场景判断是否触发 | AI 调用具体工具（function call） |
| **粒度** | 工作流级别（"遇到 bug 先排查"） | 操作级别（"解析这个抖音链接"） |

## 通俗类比

- **Skill** = 给厨师的菜谱。"做宫保鸡丁时，先切鸡丁，再炒花生。"
- **MCP** = 厨房里的锅。"这个锅可以炒菜，那个烤箱可以烘焙。"

菜谱（Skill）告诉厨师怎么用锅（MCP）。

## 实际案例

以 `douyin-mcp` 和 `douyin-to-llm-wiki-raw` 为例：

- `douyin-mcp` **MCP Server**：提供 `parse_douyin_video_info`、`extract_douyin_text` 等工具。
- `douyin-mcp` **Skill**：规定"遇到抖音链接时，优先用 MCP 工具而不是本地脚本"。
- `douyin-to-llm-wiki-raw` **Skill**：规定"获取转写后，写入 LLM Wiki raw txt，不要写总结"。

**Skill 编排流程，MCP 执行操作。**

## 什么时候用哪个

- 需要**外部能力**（查数据库、调 API、解析链接）→ MCP
- 需要**行为规范**（怎么写代码、怎么审查、怎么归档）→ Skill
- **最佳实践**：Skill 里引用 MCP 工具，形成"规则驱动工具"的闭环。

## 相关页面

- [Agent Skill](../concepts/agent-skill.md)
- [Model Context Protocol](../concepts/model-context-protocol.md)
- [MCP Tools Resources Prompts](../concepts/mcp-tools-resources-prompts.md)
