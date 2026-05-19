---
title: LLM Wiki
type: concept
status: active
updated: 2026-05-15
sources:
  - raw/sources/2026-04-04-karpathy-llm-wiki.source.md
---

# LLM Wiki

## 一句话说明

LLM Wiki 是一层由 Markdown 页面组成的知识层，既让人直接阅读，也让 AI 代理稳定检索、引用、维护和更新。

## 核心结构

- `raw/`：保存原始资料或来源记录，负责事实可追溯。
- `wiki/`：保存整理后的知识页面，负责日常查询、推理和复用。
- `schema/`：约定页面类型、字段和状态。
- `AGENTS.md`：告诉 AI 代理如何读、写、导入、查询和整理。
- `index.md`：作为人和 AI 的共同导航入口。
- `log.md`：记录知识库的维护历史。

## 与普通 RAG 的区别

普通 RAG 更像是“提问时临时检索资料”。LLM Wiki 更像是“先把资料整理成一层可维护知识，再在这层知识上查询和迭代”。

这并不排斥 RAG。页面数量变多后，`wiki/` 可以接入全文检索、向量检索或 MCP。但最小版本应该先让 Markdown 层本身可读、可维护、可追溯。

## 适用范围

适合：

- 个人知识库。
- 研究资料整理。
- 项目文档和架构知识沉淀。
- 团队 SOP、术语表、FAQ 和决策记录。
- 需要长期被 AI 代理读取和更新的知识系统。

不适合：

- 只需要一次性问答的临时资料。
- 必须强权限隔离的大型企业知识库。
- 完全依赖实时数据的场景。

## 维护方式

最小工作流是：

1. `ingest`：把资料放入 `raw/`，生成或更新 `wiki/` 页面。
2. `query`：从 `index.md` 找到相关页面，必要时回到 `raw/` 核实。
3. `lint`：检查断链、孤立页面、重复页面、无来源页面和过期页面。
4. `maintenance`：新增或大幅更新页面后，同步 `index.md`、`llms.txt`、`log.md`，并补充关键显式链接。

## 与 RAG 和 MCP 的关系

LLM Wiki 不是 RAG 或 MCP 的替代品。它更像一层已整理、可追溯、可维护的知识层。

- 页面数量较少时，AI 可以直接读取 `index.md` 和相关 Markdown 页面。
- 页面数量变多后，可以用 [Retrieval-Augmented Generation](retrieval-augmented-generation.md) 或全文搜索检索 `wiki/` 和 `raw/`。
- 需要让外部 AI 应用稳定访问这套知识库时，可以用 [Model Context Protocol](model-context-protocol.md) 暴露只读 Resource 或搜索 Tool。

## 关联页面

- [Karpathy LLM Wiki 来源总结](../sources/karpathy-llm-wiki.md)
- [RAG 学习地图](../syntheses/rag-learning-map.md)
- [MCP 学习地图](../syntheses/mcp-learning-map.md)
- [Retrieval-Augmented Generation](retrieval-augmented-generation.md)
- [Model Context Protocol](model-context-protocol.md)
- [维护规约](../../AGENTS.md)

## 待核实

- 后续如果接入 MCP，需要重新定义工具接口和权限边界。
