---
title: Chunking
type: concept
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-rag-survey.source.md
  - raw/sources/2026-05-15-raptor.source.md
---

# Chunking

## 一句话说明

Chunking 是把长文档拆成可检索片段的过程，是 RAG 检索质量的基础设计。

## 要点

- chunk 是检索系统返回给模型的基本证据单元。
- chunk 太小会丢失上下文，模型拿到片段后可能无法理解完整含义。
- chunk 太大会降低检索精度，也会浪费上下文窗口。
- 常见策略包括固定长度切块、按标题切块、按语义切块、滑动窗口和层级切块。
- RAPTOR 代表一种高级思路：通过递归聚类和摘要构建多层树状索引，让系统能从不同抽象层级检索。

## 常见策略

| 策略 | 适合场景 | 风险 |
|---|---|---|
| 固定长度切块 | 快速原型、结构弱的文本 | 容易切断语义 |
| 按标题切块 | 技术文档、Markdown、报告 | 章节过长时仍需二次切分 |
| 滑动窗口 | 需要保留邻近上下文 | 索引冗余增加 |
| 语义切块 | 段落边界清晰的资料 | 实现复杂度更高 |
| 层级切块 | 长文档、多层级资料 | 维护和评估成本更高 |

## 适用范围

适合：

- 设计文档型 RAG 系统。
- 调试「检索到了但答案仍然不准」的问题。
- 处理 PDF、论文、课程笔记、技术文档等长资料。

不适合：

- 把所有资料强行切成同样大小。
- 忽略标题、表格、代码块和列表结构。
- 只看 chunk 数量，不评估检索命中质量。

## 关联页面

- [RAG Pipeline](rag-pipeline.md)
- [Embedding](embedding.md)
- [RAPTOR](../sources/raptor.md)
- [RAG 学习地图](../syntheses/rag-learning-map.md)

## 待核实

- 具体 chunk 大小需要结合模型上下文窗口、文档结构、查询类型和评估结果确定。
