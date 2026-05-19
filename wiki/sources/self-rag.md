---
title: Self-RAG
type: source
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-05-15-self-rag.source.md
---

# Self-RAG

## 来源

- 作者：Akari Asai et al.
- 发布时间：2023-10-17
- URL：https://arxiv.org/abs/2310.11511
- 本地来源记录：`raw/sources/2026-05-15-self-rag.source.md`

## 核心内容

- Self-RAG 关注自适应检索，而不是对所有问题固定检索固定数量的 passages。
- 它引入自我反思思路，让模型判断是否需要检索、检索内容是否相关、生成内容是否被支持。
- 论文目标是提高事实性、可控性和引用准确性。

## 可转化页面

- 问题：[为什么 RAG 仍然会幻觉](../questions/why-rag-still-hallucinates.md)
- 综合：[RAG 学习地图](../syntheses/rag-learning-map.md)

## 待核实

- Self-RAG 的训练细节和 reflection tokens 机制如需深入学习，需要单独拆成概念页。
