# schema

`schema/` 定义本 Wiki 的页面类型和字段约定。它不是数据库 schema，而是让人和 AI 在维护 Markdown 页面时保持一致。

## 页面类型

- `concept`：概念页，解释一个术语、模式或方法。
- `entity`：实体页，记录人物、组织、项目、产品、论文等对象。
- `source`：来源页，总结一份原始资料。
- `synthesis`：综合页，把多个来源合并成主题综述。
- `question`：问题页，沉淀反复出现的查询、决策或未解问题。

## 分类决策表

新增页面前，先按下面的问题判断归类。不要按“看起来像什么”归类。

分类之前必须先查重：用中文名、英文名、缩写、同义词和上位概念在 `wiki/` 中搜索。已有类似页面时，优先更新旧页、补充来源和关联链接；只有新内容回答的问题明显不同，才新建页面。

| 判断问题 | 页面类型 | 放置目录 |
|---|---|---|
| 这是一个术语、方法、模式、技术能力或抽象概念吗？ | `concept` | `wiki/concepts/` |
| 这是一个具体的人、组织、项目、产品、论文、标准、工具或系统吗？ | `entity` | `wiki/entities/` |
| 这是对某一份原始资料的摘要、提取和来源说明吗？ | `source` | `wiki/sources/` |
| 这是把多个来源或多个页面整合成路线图、对比、综述或主题总结吗？ | `synthesis` | `wiki/syntheses/` |
| 这是一个用户会反复问、需要给出判断或决策的问题吗？ | `question` | `wiki/questions/` |

## 类型边界

### concept：概念页

用于解释“是什么、为什么重要、怎么使用、边界是什么”。

适合：

- 技术概念：`Retrieval-Augmented Generation`、`Embedding`、`Chunking`。
- 方法模式：`RAG Pipeline`、`Hybrid Search`。
- 能力抽象：`MCP Tools、Resources 和 Prompts`。

不适合：

- 单篇论文或文章摘要，放 `source`。
- 某个具体产品或项目，放 `entity`。
- 多个概念的学习路线，放 `synthesis`。
- “我该怎么选”的决策问题，放 `question`。

命名建议：使用稳定名词，不用疑问句。英文技术名可以保留英文。

### entity：实体页

用于记录稳定对象本身，包括人物、组织、产品、项目、论文、标准、库、工具。

适合：

- 人物：`Andrej Karpathy`。
- 组织：`OpenAI`、`Anthropic`。
- 产品或工具：`Obsidian`、`YoudaoNote CLI`。
- 论文或标准作为对象本身：`Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks`。

不适合：

- 从一篇文章中提炼的内容摘要，放 `source`。
- 一个产品背后的通用技术概念，放 `concept`。
- 多个实体的横向比较，放 `synthesis` 或 `question`。

命名建议：使用官方名称或最常见名称。

### source：来源页

用于总结“某一份原始资料说了什么”。它必须能追溯到 `raw/sources/` 或 `raw/files/`。

适合：

- 一篇论文的摘要。
- 一篇官方文档的摘要。
- 一篇博客、网页、会议纪要、导出笔记的摘要。
- 一个 PDF、PPT、视频转写的来源总结。

不适合：

- 跨多个来源的综合观点，放 `synthesis`。
- 抽象概念解释，放 `concept`。
- 用户决策问答，放 `question`。

命名建议：标题能对应原始资料，页面中必须写清来源、URL 或本地文件路径。

### synthesis：综合页

用于把多个来源和多个页面整合成更高层次的结构。

适合：

- 学习地图。
- 主题综述。
- 多方案比较。
- 路线图。
- 架构总览。

不适合：

- 单一概念解释，放 `concept`。
- 单一来源摘要，放 `source`。
- 一个可直接回答的问题，放 `question`。

命名建议：使用“学习地图”“综述”“对比”“路线图”“总览”等明确综合性质的标题。

### question：问题页

用于沉淀会反复出现的问题。它的目标是给出可复用的判断，而不是记录一个术语。

适合：

- `MCP 和 RAG 的区别是什么`。
- `为什么 RAG 仍然会幻觉`。
- `RAG 和 Fine-tuning 怎么选`。
- `什么时候该把资料录入 LLM Wiki`。

不适合：

- 只是解释一个名词，放 `concept`。
- 只是总结一篇来源，放 `source`。
- 很临时、不会复用的一次性问题，不建正式页。

命名建议：使用自然问题句，便于人和 AI 直接检索。

## 归类优先级

如果一个内容看起来能放多个目录，按以下顺序判断：

1. 先问它是不是“单一来源摘要”。是则放 `source`。
2. 再问它是不是“具体对象”。是则放 `entity`。
3. 再问它是不是“抽象概念”。是则放 `concept`。
4. 再问它是不是“多个来源/多个页面的综合”。是则放 `synthesis`。
5. 最后问它是不是“可复用问题”。是则放 `question`。

如果仍然不确定，先不要建正式页面。可以在 `wiki/questions/` 建一个 `status: seed` 的问题页，或者在相关页面的 `待核实` 中记录归类疑问。

## 典型拆分方式

一份高价值资料通常会拆成多类页面，而不是只进一个页面：

```text
raw/sources/example.source.md
  ↓
wiki/sources/example.md          # 这份资料说了什么
wiki/concepts/key-concept.md     # 资料中出现的稳定概念
wiki/entities/key-project.md     # 资料中出现的稳定对象
wiki/questions/key-decision.md   # 资料支持回答的复用问题
wiki/syntheses/topic-map.md      # 多个来源共同形成的综合页面
```

## 状态

- `seed`：初始草稿，内容还少。
- `active`：正在维护，适合日常使用。
- `stable`：较稳定，短期不需要频繁更新。
- `stale`：可能过期，需要复核。

## Front Matter

```yaml
---
title: 页面标题
type: concept | entity | source | synthesis | question
status: seed | active | stable | stale
updated: YYYY-MM-DD
sources:
  - raw/sources/example.source.md
---
```
