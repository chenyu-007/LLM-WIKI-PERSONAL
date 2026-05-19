# LLM Wiki 维护日志

本文件只追加，不重写历史。每条记录说明日期、动作、影响范围和来源。

## 2026-05-15 初始化

- 创建 Karpathy 原始模式的本地 LLM Wiki 骨架。
- 建立 `raw/`、`wiki/`、`schema/`、`templates/` 分层。
- 添加 `AGENTS.md`，定义 AI 代理进入顺序和 `ingest / query / lint` 工作流。
- 添加 Karpathy LLM Wiki gist 的来源记录与概念页。

## 2026-05-15 导入 MCP 第一批页面

- 按权威来源校准流程导入 MCP 官方介绍、架构说明和 Server Concepts 来源记录。
- 为 `MCP vs RAG` 对比页补充 RAG 原始论文来源记录。
- 新增 MCP 来源页：`wiki/sources/mcp-official-intro.md`、`wiki/sources/mcp-official-architecture.md`、`wiki/sources/mcp-official-server-concepts.md`。
- 新增 MCP 概念页：`wiki/concepts/model-context-protocol.md`、`wiki/concepts/mcp-tools-resources-prompts.md`。
- 新增 MCP 问题页和综合页：`wiki/questions/mcp-vs-rag.md`、`wiki/syntheses/mcp-learning-map.md`。
- 更新 `index.md` 和 `llms.txt`，让人和 AI 都能从入口页定位新增页面。

## 2026-05-15 导入 RAG 第一批页面

- 按权威来源校准流程导入 RAG 原始论文、RAG 大模型综述、Self-RAG、RAPTOR、GraphRAG 和 AWS RAG vs Fine-tuning 来源。
- 新增 RAG 来源页：`wiki/sources/rag-original-paper.md`、`wiki/sources/rag-survey.md`、`wiki/sources/self-rag.md`、`wiki/sources/raptor.md`、`wiki/sources/graphrag.md`、`wiki/sources/aws-rag-vs-fine-tuning.md`。
- 新增 RAG 概念页：`wiki/concepts/retrieval-augmented-generation.md`、`wiki/concepts/rag-pipeline.md`、`wiki/concepts/chunking.md`、`wiki/concepts/embedding.md`、`wiki/concepts/hybrid-search.md`、`wiki/concepts/reranker.md`。
- 新增 RAG 问题页和综合页：`wiki/questions/why-rag-still-hallucinates.md`、`wiki/questions/rag-vs-fine-tuning.md`、`wiki/syntheses/rag-learning-map.md`。
- 更新 `index.md` 和 `llms.txt`，让后续查询能从入口页定位 RAG 主题。

## 2026-05-15 新增 Quartz HTML 阅读层

- 在相邻目录 `../llm-wiki-site/` 新增独立 Quartz 工程，用于把 `llm-wiki/` Markdown 自动构建成 HTML 阅读站点。
- `llm-wiki/` 仍然是唯一知识源，`llm-wiki-site/public/` 是可删除、可重建的生成物。
- 为兼容 Quartz 的 YAML 解析，给 4 个 raw 来源记录中包含冒号的 `title` 字段补充引号。
- 在 `README.md` 补充 HTML 阅读层说明。

## 2026-05-16 导入 Tavily 和 Browserbase

- 按权威来源校准流程导入 Tavily Docs 和 Browserbase Docs 两个来源记录。
- 新增来源页：`wiki/sources/tavily-docs.md`、`wiki/sources/browserbase-docs.md`。
- 新增实体页：`wiki/entities/tavily.md`、`wiki/entities/browserbase.md`。
- 新增问题页：`wiki/questions/tavily-vs-browserbase.md`，用于区分 AI Search API 和云浏览器自动化平台。
- 更新 `index.md` 和 `llms.txt`，让后续查询能从入口页定位这两个工具。

## 2026-05-15 执行维护闭环

- 在 `AGENTS.md` 中补充 `maintenance` 工作流，明确导入后的索引、补链、日志和断链检查要求。
- 为 `LLM Wiki` 概念页补充与 RAG、MCP 和维护闭环的关系说明。
- 为 RAG/MCP 学习地图、核心概念页和问题页补充关键显式链接。
- 同步 `llms.txt` 的核心页面和维护规则入口。
- 执行 Markdown 链接检查和页面入链/出链统计。

## 2026-05-15 补充页面分类规则

- 扩展 `schema/README.md`，补充 `concept`、`entity`、`source`、`synthesis`、`question` 的判断标准、边界和命名建议。
- 更新 `wiki/README.md`，增加日常快速归类说明。
- 更新 `AGENTS.md` 的 `ingest` 流程，要求 AI 在建页前先读取分类决策表。

## 2026-05-16 导入有道云笔记审核通过知识点

- 按用户确认的审核报告处理有道云笔记条目 2、7、11、12、13、14、15。
- 录入前检查现有 `wiki/` 页面，避免重复创建 RAG、Embedding、RAG Pipeline 等已有词条；已有词条采用更新方式。
- 更新 RAG 相关页面：`wiki/concepts/retrieval-augmented-generation.md`、`wiki/concepts/rag-pipeline.md`、`wiki/concepts/embedding.md`、`wiki/concepts/vector-database.md`、`wiki/syntheses/rag-vs-llm-wiki.md`。
- 新增 MySQL 相关页面：`wiki/concepts/mysql-explain.md`、`wiki/concepts/sql-indexing.md`、`wiki/concepts/mysql-transaction-isolation.md`、`wiki/concepts/mvcc.md`、`wiki/concepts/gorm-transaction.md`、`wiki/questions/how-to-diagnose-a-slow-mysql-query.md`、`wiki/questions/why-mysql-repeatable-read-is-not-the-same-as-snapshot-isolation.md`。
- 新增 Redis 相关页面：`wiki/concepts/redis-data-types.md`、`wiki/concepts/redis-persistence.md`、`wiki/concepts/redis-acl.md`、`wiki/concepts/redis-scan.md`、`wiki/concepts/redis-big-key-deletion.md`。
- 新增 OpenFaaS、Kubernetes、Elasticsearch 相关页面，并把不确定的源码级实现细节保留在待核实中。
- 更新 `AGENTS.md`，将“新建词条前查重，已有类似词条优先更新旧页”写入 ingest 规则。
- 更新 `schema/README.md`，将查重放到分类决策之前，要求先搜索中文名、英文名、缩写、同义词和上位概念。
- 更新 `index.md` 和 `llms.txt`，让人和 AI 能从入口页定位新增页面。
