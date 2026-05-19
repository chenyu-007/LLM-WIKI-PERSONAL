---
source: youdao-note-batch
captured: 2026-05-15
status: accepted-ingested
scope: "approved items 2, 7, 11, 12, 13, 14, 15"
approved: 2026-05-16
ingested: 2026-05-16
---

# 有道云笔记候选知识点审核报告

本报告只处理用户批准的 7 个条目：2、7、11、12、13、14、15。

处理原则：

- 不照搬原笔记，只抽取值得沉淀的知识点。
- 原笔记作为线索，正式写入 `wiki/` 前必须以官方文档、论文或一手资料校验。
- 本文件仍属于 `raw/inbox/`，不是正式 LLM Wiki 页面。
- 下面所有“建议录入”都还需要用户确认后才能进入正式 `wiki/`。

## 总览

| 编号 | 原始文件 | 审核结论 | 建议动作 |
| --- | --- | --- | --- |
| 2 | `02-openfaas-gateway-request-chain.md` | 有价值，适合作为 OpenFaaS 请求链路线索 | 部分录入，保留官方概念，代码级函数名需另行按仓库版本校验 |
| 7 | `07-retrieval-augmented-generation.md` | 有价值，但 MCP 段存在明显错误 | 只录入 RAG 主干知识；MCP 相关内容重写，不按原文录入 |
| 11 | `11-openfaas-kind-kubernetes-namespace.md` | 有价值，但标题与内容不符 | 改名后录入 OpenFaaS + kind + Kubernetes namespace 相关知识 |
| 12 | `12-mysql-sql-tuning.md` | 有价值，适合整理成 SQL 调优 checklist | 录入时弱化绝对化表述，补充 MySQL 官方语义 |
| 13 | `13-mysql-transaction-isolation.md` | 有价值，但有若干错误 | 修正后录入事务、隔离级别、GORM 事务知识 |
| 14 | `14-elasticsearch-architecture.md` | 有价值，整体可靠 | 录入 ES 架构基础，术语更新为 Data View |
| 15 | `15-redis-basics.md` | 有价值，但若干点需要纠正 | 修正后录入 Redis 数据类型、持久化、ACL、遍历和大 key 删除 |

## 2. OpenFaaS 网关函数请求全链路

来源文件：`02-openfaas-gateway-request-chain.md`

建议知识点：

- OpenFaaS Gateway 是函数调用、管理 API、UI/Portal 的入口。
- 同步调用通常走 `/function/` 路由；异步调用走 `/async-function` 路由。
- Gateway 与 provider、function Pod、副本数、指标、自动伸缩之间存在明确职责边界。
- OpenFaaS 的伸缩能力可以基于函数标签配置，官方标签包括 `com.openfaas.scale.type`、`com.openfaas.scale.target`、`com.openfaas.scale.min`、`com.openfaas.scale.max`、`com.openfaas.scale.zero` 等。
- OpenFaaS 通过 Gateway 观察到的同步和异步调用都可参与自动伸缩判断。

不要直接录入的点：

- `MakeScalingHandler`、`FunctionScaler.Scale`、`singleflight`、具体源码文件路径等属于某个源码版本的实现细节。可以作为“源码阅读问题”保留，但写入正式 wiki 前需要对当前 OpenFaaS 仓库版本逐项校验。
- `com.openfaas.memory-size`、`com.openfaas.cold-start-cost` 更像项目自定义 annotation，不应写成 OpenFaaS 官方标签。

建议页面：

- `sources/youdao-openfaas-gateway-request-chain.md`
- `concepts/openfaas-gateway.md`
- `questions/openfaas-function-invocation-path.md`

## 7. 检索增强生成（RAG）

来源文件：`07-retrieval-augmented-generation.md`

建议知识点：

- RAG 的核心是把参数化模型能力与外部非参数化知识源结合：先检索相关材料，再让模型基于检索结果生成。
- 典型 RAG 流程可拆成：文档切分、向量化、索引入库、查询向量化、相似度检索、重排或过滤、上下文组装、生成回答。
- Embedding 把文本映射为向量，向量相似度检索用于查找语义相关片段。
- 向量数据库的关键能力包括向量索引、相似度搜索、元数据过滤、命名空间或集合管理。
- RAG 和 LLM Wiki 的定位不同：RAG 偏自动检索和运行时注入；LLM Wiki 偏人工/AI 共同维护的高信噪比知识基底。两者可以互补，不是互相替代。

需要重写或排除的点：

- 原笔记里“RAG 是 MCP 的子集”“目前没有官方 MCP 标准”“Google MCP”等表述不可靠。MCP 现在有公开规格，核心对象包括 clients、servers、tools、resources、prompts 等；RAG 只是可通过 MCP 暴露的一类检索能力，不是 MCP 的子集。
- MCP 段应该单独作为“待重写问题页”，不要从这条 RAG 笔记中直接导入。
- 医疗咨询示例涉及高风险领域，不建议作为 wiki 的默认示例。可以改成低风险的企业文档检索或代码库问答示例。

建议页面：

- `concepts/retrieval-augmented-generation.md`
- `concepts/embedding.md`
- `concepts/vector-database.md`
- `syntheses/rag-vs-llm-wiki.md`
- `questions/how-to-build-a-minimal-rag-pipeline.md`

## 11. OpenFaaS、kind 与 Kubernetes namespace

来源文件：`11-openfaas-kind-kubernetes-namespace.md`

标题问题：

- 原标题含 “rust-mobile”，但正文主要是 OpenFaaS、kind、Kubernetes namespace 和本地端口映射。正式录入时应改名。

建议知识点：

- Kubernetes namespace 用于在同一集群中隔离一组资源名称和访问边界。
- OpenFaaS 常见部署中会区分控制平面 namespace 与函数 namespace，例如 `openfaas` 和 `openfaas-fn`。
- kind 的 `extraPortMappings` 可以把宿主机端口映射到 kind 节点端口，常用于本地暴露 NodePort 服务。
- 本地访问链路可以整理为：宿主机端口 -> kind 节点端口 -> Kubernetes Service -> Gateway Pod。

需要谨慎的点：

- “faas-netes controller 编译进 gateway”不宜直接写入。OpenFaaS 的 provider 形态和实现会随版本变化，正式录入前要按目标版本源码确认。
- 端口 `8080`、`31112` 只是当前部署示例，不是通用标准。

建议页面：

- `sources/youdao-openfaas-kind-namespace.md`
- `concepts/kubernetes-namespace.md`
- `questions/how-kind-exposes-openfaas-gateway-locally.md`

## 12. MySQL SQL 调优专项

来源文件：`12-mysql-sql-tuning.md`

建议知识点：

- SQL 调优应先定位问题：慢查询日志、APM、数据库监控、`EXPLAIN` / `EXPLAIN ANALYZE`。
- `EXPLAIN` 可关注访问类型、候选索引、实际使用索引、扫描行数、过滤比例、Extra 信息。
- 常见优化方向：为过滤、连接、排序、分组设计合适索引；避免不必要的 `SELECT *`；减少 N+1 查询；谨慎使用大 `IN`；避免在索引列上包函数导致索引不可用。
- `ORDER BY` / `GROUP BY` 能否利用索引，取决于索引设计、查询条件和优化器判断。

需要修正的点：

- `Using filesort` 不等于一定“磁盘排序”。它表示 MySQL 需要额外排序步骤，可能在内存或磁盘完成。
- `Using temporary` 是性能警告信号，但不能简单写成“性能极差”。是否严重取决于数据量、临时表类型、内存配置和查询形态。
- `EXPLAIN` 与 `EXPLAIN ANALYZE` 要区分：后者会实际执行并给出运行时信息。

建议页面：

- `concepts/mysql-explain.md`
- `concepts/sql-indexing.md`
- `questions/how-to-diagnose-a-slow-mysql-query.md`

## 13. MySQL 事务与隔离级别

来源文件：`13-mysql-transaction-isolation.md`

建议知识点：

- 事务的基本目标是把一组操作作为一个逻辑单元提交或回滚。
- ACID 可以作为事务语义的入口解释：Atomicity、Consistency、Isolation、Durability。
- MySQL InnoDB 支持常见隔离级别：Read Uncommitted、Read Committed、Repeatable Read、Serializable。
- MySQL InnoDB 默认隔离级别是 Repeatable Read。
- Repeatable Read 下，普通一致性读依赖 MVCC read view；锁定读和写操作会涉及记录锁、间隙锁或 next-key locks 等机制。
- GORM 支持 `db.Transaction` 风格的事务，也支持 savepoint/rollback to savepoint。

需要修正的点：

- 原笔记 SQL 里有拼写错误：`ISLATION` 应为 `ISOLATION`。
- “主流数据库默认 Read Committed”不能用于 MySQL。MySQL InnoDB 默认是 Repeatable Read。
- “GORM 默认不支持嵌套事务”表述不准确。GORM 官方文档包含 nested transaction 和 savepoint 示例。
- 幻读问题不要只写成“RR 完全靠 next-key lock 防止”。普通一致性读与锁定读语义不同，需要分开讲。

建议页面：

- `concepts/mysql-transaction-isolation.md`
- `concepts/mvcc.md`
- `concepts/gorm-transaction.md`
- `questions/why-mysql-repeatable-read-is-not-the-same-as-snapshot-isolation.md`

## 14. Elasticsearch 架构

来源文件：`14-elasticsearch-architecture.md`

建议知识点：

- Elasticsearch 的核心层次可以从 Cluster、Node、Index、Shard、Document 理解。
- Shard 是索引的分片单元，primary shard 与 replica shard 共同影响容量、可用性和查询并发。
- Document 是 Elasticsearch 的基本可索引数据单元，字段结构由 mapping 管理。
- Kibana 现在更推荐使用 Data View 这一术语；旧文档或旧版本里常见 Index Pattern。
- Prometheus 更适合时序指标监控；Elasticsearch 更适合日志、文档、全文检索和分析，二者解决的问题不同。

需要修正或补充的点：

- “Index 类似数据库表”只能作为初学类比，不应写成严格等价。Elasticsearch 7 之后 type 被移除，这个类比更容易误导。
- 需要补充 mapping、倒排索引、refresh、near real-time search 这些更核心的 ES 概念，原笔记覆盖不够。

建议页面：

- `concepts/elasticsearch-architecture.md`
- `concepts/elasticsearch-shard.md`
- `concepts/kibana-data-view.md`
- `syntheses/prometheus-vs-elasticsearch.md`

## 15. Redis 常识

来源文件：`15-redis-basics.md`

建议知识点：

- Redis 是数据结构服务器，不是关系型表结构；一个 key 对应一个带类型的 value。
- Redis 常见数据类型包括 String、Hash、List、Set、Sorted Set、Stream、Bitmap、HyperLogLog 等。
- String 是二进制安全的字节序列，也可承载计数器、缓存值、位图等用法。
- Redis 持久化取决于配置，主要机制包括 RDB、AOF 或两者结合。
- Redis 6 起 ACL 能做更细粒度的用户、命令、key pattern 权限控制。
- 遍历 keyspace 时应优先理解 `SCAN` 的增量迭代语义；`COUNT` 是提示，不是精确返回数量保证。
- 删除大 key 时可考虑 `UNLINK`，它把内存回收交给后台异步处理，降低主线程阻塞风险。

需要修正的点：

- 原笔记说“对同一个 key 先 SET 再 HSET 会直接覆盖并改变类型，不报错”是错误的。已存在 string key 时执行 hash 命令通常会返回 WRONGTYPE；要改类型需要先删除、覆盖为目标类型或使用对应命令语义。
- “重启默认丢数据”不能作为通用事实。是否丢数据取决于 RDB/AOF 配置和写入时机。
- “Redis 选择跳表是因为适合并发”容易误导。Redis 命令执行主要是单线程模型，Sorted Set 使用 skiplist 主要是为了有序范围查询、插入删除复杂度和实现权衡。
- List 底层实现要标注版本差异：旧资料常讲 quicklist + ziplist，新版本内部结构已演进，不能写成永久事实。

建议页面：

- `concepts/redis-data-types.md`
- `concepts/redis-persistence.md`
- `concepts/redis-acl.md`
- `concepts/redis-scan.md`
- `concepts/redis-big-key-deletion.md`

## 建议优先录入顺序

第一批建议录入：

1. `concepts/retrieval-augmented-generation.md`
2. `syntheses/rag-vs-llm-wiki.md`
3. `concepts/mysql-explain.md`
4. `concepts/mysql-transaction-isolation.md`
5. `concepts/redis-data-types.md`

第二批建议录入：

1. `concepts/openfaas-gateway.md`
2. `questions/openfaas-function-invocation-path.md`
3. `concepts/elasticsearch-architecture.md`
4. `concepts/kubernetes-namespace.md`
5. `concepts/redis-persistence.md`

## 暂不建议录入

- RAG 笔记中关于 MCP 的整段原始表述。
- OpenFaaS 笔记中未按目标版本源码校验的具体函数名与本地路径。
- Redis 笔记中关于 key 类型自动覆盖、跳表为了并发、默认重启必丢数据的表述。

## 校验来源

- OpenFaaS Gateway：<https://docs.openfaas.com/architecture/gateway/>
- OpenFaaS Invocations：<https://docs.openfaas.com/architecture/invocations/>
- OpenFaaS Async：<https://docs.openfaas.com/reference/async/>
- OpenFaaS Autoscaling：<https://docs.openfaas.com/architecture/autoscaling/>
- OpenFaaS Namespaces：<https://docs.openfaas.com/reference/namespaces/>
- Kubernetes Namespaces：<https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/>
- kind Configuration：<https://kind.sigs.k8s.io/docs/user/configuration/>
- MySQL EXPLAIN Output：<https://dev.mysql.com/doc/refman/8.4/en/explain-output.html>
- MySQL InnoDB Transaction Isolation Levels：<https://dev.mysql.com/doc/refman/8.4/en/innodb-transaction-isolation-levels.html>
- MySQL SET TRANSACTION：<https://dev.mysql.com/doc/refman/8.4/en/set-transaction.html>
- GORM Transactions：<https://gorm.io/docs/transactions.html>
- Elastic Clusters, Nodes, and Shards：<https://www.elastic.co/docs/deploy-manage/distributed-architecture/clusters-nodes-shards>
- Kibana Data Views：<https://www.elastic.co/docs/explore-analyze/find-and-organize/data-views>
- Redis Data Types：<https://redis.io/docs/latest/develop/data-types/>
- Redis Persistence：<https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/>
- Redis ACL：<https://redis.io/docs/latest/operate/oss_and_stack/management/security/acl/>
- Redis SCAN：<https://redis.io/docs/latest/commands/scan/>
- Redis UNLINK：<https://redis.io/docs/latest/commands/unlink/>
- RAG 原论文：<https://arxiv.org/abs/2005.11401>
- OpenAI Embeddings：<https://developers.openai.com/api/docs/guides/embeddings>
- Pinecone Overview：<https://docs.pinecone.io/guides/get-started/overview>
- Model Context Protocol Specification：<https://modelcontextprotocol.io/specification/2025-06-18>

## 用户确认与处理结果

用户已在 2026-05-16 确认执行。已按本报告建议创建或更新正式 `wiki/` 页面，并在页面中保留来源、校验依据、反向链接和未确认事项。
