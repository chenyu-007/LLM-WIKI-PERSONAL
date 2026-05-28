# LLM Wiki 索引

本索引是人和 AI 共用的入口页。查询前先看这里，再进入具体页面。

## 快速入口

- [LLM Wiki 概念](wiki/concepts/llm-wiki.md)
- [Model Context Protocol](wiki/concepts/model-context-protocol.md)
- [MCP 学习地图](wiki/syntheses/mcp-learning-map.md)
- [Retrieval-Augmented Generation](wiki/concepts/retrieval-augmented-generation.md)
- [RAG 学习地图](wiki/syntheses/rag-learning-map.md)
- [RAG 和 LLM Wiki 怎么配合](wiki/syntheses/rag-vs-llm-wiki.md)
- [Tavily](wiki/entities/tavily.md)
- [Browserbase](wiki/entities/browserbase.md)
- [MySQL 慢查询诊断](wiki/questions/how-to-diagnose-a-slow-mysql-query.md)
- [Redis 数据类型](wiki/concepts/redis-data-types.md)
- [AI 知识库全景图](wiki/syntheses/ai-knowledge-map.md)
- [AI Agent 概念](wiki/concepts/ai-agent.md)
- [Agent Memory 长期记忆](wiki/concepts/agent-memory.md)
- [Agent Skill 概念](wiki/concepts/agent-skill.md)
- [Agent Skill vs MCP](wiki/questions/agent-skill-vs-mcp.md)
- [AI 工作流](wiki/concepts/ai-workflow.md)
- [Anthropic Agent Engineering 学习地图](wiki/syntheses/anthropic-agent-engineering-map.md)
- [Karpathy LLM Wiki 来源总结](wiki/sources/karpathy-llm-wiki.md)
- [原始来源记录](raw/sources/2026-04-04-karpathy-llm-wiki.source.md)
- [维护规约](AGENTS.md)

## 页面分类

### 概念

- [LLM Wiki](wiki/concepts/llm-wiki.md)
- [Model Context Protocol](wiki/concepts/model-context-protocol.md)
- [MCP Tools、Resources 和 Prompts](wiki/concepts/mcp-tools-resources-prompts.md)
- [Retrieval-Augmented Generation](wiki/concepts/retrieval-augmented-generation.md)
- [RAG Pipeline](wiki/concepts/rag-pipeline.md)
- [Chunking](wiki/concepts/chunking.md)
- [Embedding](wiki/concepts/embedding.md)
- [向量数据库](wiki/concepts/vector-database.md)
- [Hybrid Search](wiki/concepts/hybrid-search.md)
- [Reranker](wiki/concepts/reranker.md)
- [MySQL EXPLAIN](wiki/concepts/mysql-explain.md)
- [SQL 索引设计](wiki/concepts/sql-indexing.md)
- [MySQL 事务隔离级别](wiki/concepts/mysql-transaction-isolation.md)
- [MVCC](wiki/concepts/mvcc.md)
- [GORM 事务](wiki/concepts/gorm-transaction.md)
- [Redis 数据类型](wiki/concepts/redis-data-types.md)
- [Redis 持久化](wiki/concepts/redis-persistence.md)
- [Redis ACL](wiki/concepts/redis-acl.md)
- [Redis SCAN](wiki/concepts/redis-scan.md)
- [Redis 大 key 删除](wiki/concepts/redis-big-key-deletion.md)
- [OpenFaaS Gateway](wiki/concepts/openfaas-gateway.md)
- [Kubernetes Namespace](wiki/concepts/kubernetes-namespace.md)
- [Elasticsearch 架构](wiki/concepts/elasticsearch-architecture.md)
- [Elasticsearch Shard](wiki/concepts/elasticsearch-shard.md)
- [Kibana Data View](wiki/concepts/kibana-data-view.md)
- [Agent Skill](wiki/concepts/agent-skill.md)
- [AI Agent](wiki/concepts/ai-agent.md)
- [Agent Memory](wiki/concepts/agent-memory.md)
- [上下文工程](wiki/concepts/context-engineering.md)
- [AI 工作流](wiki/concepts/ai-workflow.md)

### 来源

- [Karpathy LLM Wiki gist](wiki/sources/karpathy-llm-wiki.md)
- [MCP 官方介绍](wiki/sources/mcp-official-intro.md)
- [MCP 官方架构说明](wiki/sources/mcp-official-architecture.md)
- [MCP 官方 Server Concepts](wiki/sources/mcp-official-server-concepts.md)
- [RAG 原始论文](wiki/sources/rag-original-paper.md)
- [RAG 大模型综述](wiki/sources/rag-survey.md)
- [Self-RAG](wiki/sources/self-rag.md)
- [RAPTOR](wiki/sources/raptor.md)
- [GraphRAG](wiki/sources/graphrag.md)
- [AWS RAG vs Fine-tuning 对比](wiki/sources/aws-rag-vs-fine-tuning.md)
- [Tavily Docs](wiki/sources/tavily-docs.md)
- [Browserbase Docs](wiki/sources/browserbase-docs.md)

### 实体

- [Tavily](wiki/entities/tavily.md)
- [Browserbase](wiki/entities/browserbase.md)
- [OpenClaw](wiki/entities/openclaw.md)
- [Claude Code](wiki/entities/claude-code.md)
- [Anthropic](wiki/entities/anthropic.md)
- [Pinecone / Nexus](wiki/entities/pinecone.md)
- [Mem0](wiki/entities/mem0.md)

### 综合

- [MCP 学习地图](wiki/syntheses/mcp-learning-map.md)
- [RAG 学习地图](wiki/syntheses/rag-learning-map.md)
- [RAG 和 LLM Wiki 怎么配合](wiki/syntheses/rag-vs-llm-wiki.md)
- [Prometheus 和 Elasticsearch 怎么区分](wiki/syntheses/prometheus-vs-elasticsearch.md)
- [AI 知识库全景图](wiki/syntheses/ai-knowledge-map.md)
- [Anthropic Agent Engineering 学习地图](wiki/syntheses/anthropic-agent-engineering-map.md)

### 问题

- [MCP 和 RAG 的区别是什么](wiki/questions/mcp-vs-rag.md)
- [为什么 RAG 仍然会幻觉](wiki/questions/why-rag-still-hallucinates.md)
- [RAG 和 Fine-tuning 怎么选](wiki/questions/rag-vs-fine-tuning.md)
- [Tavily 和 Browserbase 怎么区分](wiki/questions/tavily-vs-browserbase.md)
- [如何诊断 MySQL 慢查询](wiki/questions/how-to-diagnose-a-slow-mysql-query.md)
- [为什么 MySQL Repeatable Read 不等于简单快照隔离](wiki/questions/why-mysql-repeatable-read-is-not-the-same-as-snapshot-isolation.md)
- [OpenFaaS 函数调用路径怎么理解](wiki/questions/openfaas-function-invocation-path.md)
- [kind 本地如何暴露 OpenFaaS Gateway](wiki/questions/how-kind-exposes-openfaas-gateway-locally.md)
- [Agent Skill 和 MCP 最根本的差异](wiki/questions/agent-skill-vs-mcp.md)
- [PRD 还是原型](wiki/questions/prototype-vs-prd.md)

## 当前维护重点

- 先保持结构简单，验证 `raw/`、`wiki/`、`index.md`、`log.md` 四件事是否顺手。
- 每次新增资料时，都要留下来源记录和日志。
- 新建词条前必须先查重；已有类似词条时优先更新旧页，不重复建页。
- 页面数量变多后，再考虑自动化 `lint` 和 MCP 接入。
