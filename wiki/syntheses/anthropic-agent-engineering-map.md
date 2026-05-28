---
title: Anthropic Agent Engineering 学习地图
type: synthesis
status: seed
updated: 2026-05-28
sources:
  - raw/sources/2026-05-28-anthropic-engineering.source.md
  - raw/sources/2026-05-28-anthropic-newsroom.source.md
  - raw/sources/2026-05-28-anthropic-building-effective-agents.source.md
  - raw/sources/2026-05-28-anthropic-claude-code-best-practices.source.md
  - raw/sources/2026-05-28-anthropic-multi-agent-research-system.source.md
  - raw/sources/2026-05-28-anthropic-writing-tools-for-agents.source.md
  - raw/sources/2026-05-28-anthropic-context-engineering-agents.source.md
  - raw/sources/2026-05-28-anthropic-agent-skills.source.md
  - raw/sources/2026-05-28-anthropic-code-execution-with-mcp.source.md
  - raw/sources/2026-05-28-anthropic-effective-harnesses-long-running-agents.source.md
---

# Anthropic Agent Engineering 学习地图

## 一句话说明

这一页把 Anthropic 官方 Engineering / Newsroom 中和 Agent、Claude Code、MCP、Skill、上下文工程有关的资料组织成一条学习路线，作为本 Wiki 校验二手资料的官方入口。

## 来源分层

- 官方入口：[Anthropic Engineering](../../raw/sources/2026-05-28-anthropic-engineering.source.md) 用来发现 Agent 工程文章；[Anthropic Newsroom](../../raw/sources/2026-05-28-anthropic-newsroom.source.md) 用来校验产品、公司和生态动态。
- 基础方法论：[Building effective agents](../../raw/sources/2026-05-28-anthropic-building-effective-agents.source.md) 是 Agent 架构入门基准。
- 编程 Agent：[Claude Code: Best practices for agentic coding](../../raw/sources/2026-05-28-anthropic-claude-code-best-practices.source.md) 是 Claude Code 使用和 agentic coding 的实践基准。
- 多 Agent：[How we built our multi-agent research system](../../raw/sources/2026-05-28-anthropic-multi-agent-research-system.source.md) 用来判断什么时候多 Agent 值得引入。
- 工具与 MCP：[Writing effective tools for AI agents](../../raw/sources/2026-05-28-anthropic-writing-tools-for-agents.source.md) 和 [Code execution with MCP](../../raw/sources/2026-05-28-anthropic-code-execution-with-mcp.source.md) 用来设计 Agent 可用的工具边界。
- 上下文与长任务：[Effective context engineering for AI agents](../../raw/sources/2026-05-28-anthropic-context-engineering-agents.source.md) 和 [Effective harnesses for long-running agents](../../raw/sources/2026-05-28-anthropic-effective-harnesses-long-running-agents.source.md) 用来处理上下文有限、任务跨窗口接力的问题。
- 可复用能力：[Agent Skills](../../raw/sources/2026-05-28-anthropic-agent-skills.source.md) 用来校验 Skill 的格式、渐进加载和与 MCP 的关系。

## 核心吸收

- **先 workflow，后 agent**：能用确定流程解决的任务，优先做成可预测、可调试的 workflow；只有任务路径高度动态时才提升为自主 agent。
- **简单可组合优先**：Anthropic 的 Agent 文章反复强调，成功实现通常不是复杂框架，而是小而清楚的模式组合。
- **上下文是有限工程资源**：Agent 的能力不只取决于模型，也取决于它每一步能看到什么、看不到什么、什么被外化为文件。
- **工具要为 Agent 设计**：工具命名、参数、返回结果和数量都会影响 Agent 是否能正确选择和调用工具。
- **MCP 需要上下文预算**：接入太多 MCP 工具会让工具定义和中间结果占用上下文；代码执行、按需加载和结果过滤是缓解方式。
- **Skill 是可复用程序性知识**：Skill 适合保存“怎么做”的流程和资源，MCP 适合提供“能调用什么”的外部能力。
- **多 Agent 只在适合的任务上有价值**：开放式研究、广度优先搜索、可并行子问题适合多 Agent；简单线性任务过早多 Agent 会增加协调成本。
- **长任务必须留下接力工件**：跨上下文窗口的任务需要计划、状态、检查点和交接文档，否则新会话无法稳定继承旧进度。

## 对本 LLM Wiki 的意义

- `raw/` 是长期事实来源；`wiki/` 是压缩后的可读上下文。
- `AGENTS.md` 相当于本库的操作 Skill，告诉 Codex/Hermes 进入知识库后怎么读、怎么写、怎么维护。
- `index.md` 和 `llms.txt` 是给人和 AI 的短上下文入口，避免每次把全部资料塞进对话。
- 每次吸收资料都先保留官方 raw source，再把稳定结论写入 wiki；这是对上下文工程和可追溯性的本地实现。

## 关联页面

- [Anthropic](../entities/anthropic.md)
- [Claude Code](../entities/claude-code.md)
- [AI Agent](../concepts/ai-agent.md)
- [AI 工作流](../concepts/ai-workflow.md)
- [上下文工程](../concepts/context-engineering.md)
- [Agent Skill](../concepts/agent-skill.md)
- [Agent Skill vs MCP](../questions/agent-skill-vs-mcp.md)

## 待核实

- Newsroom 和 Engineering 入口会持续更新；引用“最新文章”时必须重新打开官方页面确认日期。
- 这页先作为官方资料地图，不替代逐篇 source 页；如果某篇文章后续频繁被引用，应单独创建 `wiki/sources/` 摘要页。
