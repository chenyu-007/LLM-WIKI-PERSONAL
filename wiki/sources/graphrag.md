---
title: GraphRAG
type: source
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-graphrag.source.md
---

# GraphRAG

## 来源

- 作者：Darren Edge et al.
- 发布时间：2024-04-24
- URL：https://arxiv.org/abs/2404.16130
- 本地来源记录：`raw/sources/2026-05-15-graphrag.source.md`

## 核心内容

- GraphRAG 针对的是普通 RAG 不擅长的全局问题，例如「整个数据集有哪些主要主题」。
- 论文方案先从文本中构建实体图谱，再生成社区摘要，最后把多个局部回答合成全局回答。
- 它更像是面向大语料理解和查询聚合的 RAG 结构，而不是普通点查式问答。

## 可转化页面

- 综合：[RAG 学习地图](../syntheses/rag-learning-map.md)

## 待核实

- GraphRAG 的成本和维护复杂度较高，是否用于个人知识库需要后续单独评估。
