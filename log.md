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

## 2026-05-20 补充 GitHub 同步规则

- 在 `AGENTS.md` 新增 `publish` 工作流，要求每次知识库更新完成后提交并推送到远程仓库。
- 在 `README.md` 补充“推送到 GitHub”说明，明确更新后需要先检查再 `git push`。

## 2026-05-24 维护闭环：修复欠缺项

- 为 `llms.txt` 新增 Source Summaries 章节，补全缺失的 11 个 wiki/sources/ 页面。
- 更新 wiki/entities/README.md、wiki/questions/README.md、wiki/syntheses/README.md，将当前暂无替换为已有页面列表。
- 删除空文件 doc/async_worker.md 及空目录 doc/。
- 将散落根目录的 bilibili-homepage-2026-05-17.png 归入 raw/files/。

## 2026-05-25 - Digest Douyin transcriptions

- Created `wiki/sources/乌龙过珉-在看小说推文每日更新-双男主-上热门.md` from douyin raw transcription: 📖：乌龙过珉   在🧻🐯看#小说推文每日更新 #双男主 #上热门🔥
- Created `wiki/sources/旁观心音18评分95分以上的小说-配享太庙-续集.md` from douyin raw transcription: 旁观心音18#评分9.5分以上的小说 #配享太庙 #续集
- Created `wiki/sources/居然有不卡建模的原生亚裔妆这个教程把我压箱底的换头术都拿出来了无美颜无滤镜自然光实拍每个步骤都比较详细包教包会妆教-双眼皮贴-假睫毛.md` from douyin raw transcription: 居然有不卡建模的原生亚裔妆🎀？！这个教程把我压箱底的‘换头术’都拿出来了！无美颜无滤镜，自然光实拍，每个步骤都比较详细，
- Created `wiki/sources/全程遮胎记教程视频分享来啦遮胎记-遮瑕教程-底妆教程-零基础学化妆-化妆培训-DOU上热门-DOU小助手-韩子造型明花同学自用橱窗可.md` from douyin raw transcription: 全程遮胎记教程视频分享来啦#遮胎记 #遮瑕教程 #底妆教程 #零基础学化妆 #化妆培训 @DOU+上热门 @DOU+小助
- Created `wiki/sources/持续收集验证整理真正能用-AI-产生收入的方法工具案例平台变现路径目标是让普通人也能靠-AI-实现副业主业收入这不是单纯的AI-工具列表.md` from douyin raw transcription: 持续收集、验证、整理真正能用 AI 产生收入的方法、工具、案例、平台、变现路径，目标是让普通人也能靠 AI 实现副业/主
- Created `wiki/sources/findskills帮你智能调用合适的skills-你有没有这种情况你现在想解决一个问题但不知道如何在海量的-Skills-里找到刚好能帮到你的那个这个.md` from douyin raw transcription: findskills帮你智能调用合适的skills 你有没有这种情况：你现在想解决一个问题，但不知道如何在海量的 Ski
- Created `wiki/sources/LangChain用Trace数据优化Harness-LangChain用Trace数据优化Harness-langchainImproving-Deep-A.md` from douyin raw transcription: LangChain用Trace数据优化Harness LangChain用Trace数据优化Harness-langch
- Created `wiki/sources/单体Agent起步拒绝造火箭-单体Agent起步拒绝造火箭AnthropicBuilding-Effective-AI-Agents-Architec.md` from douyin raw transcription: 单体Agent起步，拒绝造火箭 单体Agent起步，拒绝造火箭：Anthropic《Building Effective
- Created `wiki/sources/飞书官方插件一出龙虾的玩法彻底变了-OpenClaw-飞书-Agent-养虾-飞书妙搭.md` from douyin raw transcription: 飞书官方插件一出，龙虾的玩法彻底变了 #OpenClaw  #飞书  #Agent #养虾  #飞书妙搭
- Created `wiki/sources/为什么Obsidian是AI时代最佳知识管理工具-用了18年笔记软件从Evernote到Notion从Roam到logseq最终我选择了Obsidian.md` from douyin raw transcription: 为什么Obsidian是AI时代最佳知识管理工具 用了18年笔记软件,从Evernote到Notion，从Roam到lo
- Created `wiki/sources/TokenAgentMcpRAG这些词到底什么意思.md` from douyin raw transcription: Token，Agent，Mcp，RAG这些词到底什么意思？
- Created `wiki/sources/Anthropic-前几天的工程博客.md` from douyin raw transcription: Anthropic 前几天的工程博客
- Created `wiki/sources/Claude-Code上下文工程详解-ai-技术分享-Agent.md` from douyin raw transcription: Claude Code上下文工程详解 #ai #技术分享 #Agent
- Created `wiki/sources/Agent的能力上限到底在哪01-大模型应用开发AI应用开发-Anthropic-Agent开发.md` from douyin raw transcription: Agent的能力上限到底在哪？01 #大模型应用开发#AI应用开发 #Anthropic  #Agent开发
- Created `wiki/sources/面试官问说说-Agent-Skill-和-MCP-最根本的差异.md` from douyin raw transcription: 面试官问：“说说 Agent Skill 和 MCP 最根本的差异？”
- Created `wiki/sources/为什么你的skill没用-大模型应用-AI应用开发-Agent开发-Anthropic.md` from douyin raw transcription: 为什么你的skill没用？ #大模型应用 #AI应用开发 #Agent开发 #Anthropic
- Created `wiki/sources/工具已开源我的优化版-Karpathy知识库-折腾了好几天终于搞完开源了.md` from douyin raw transcription: （工具已开源）我的优化版-Karpathy知识库 折腾了好几天，终于搞完开源了
- Created `wiki/sources/跟Karpathy学搭建AI知识库-Obsidian实践-KarpathyOpenAI创始人之一特斯拉前AI总监最近发了个LLM-Wiki框架3天500.md` from douyin raw transcription: 跟Karpathy学搭建AI知识库-Obsidian实践 Karpathy（OpenAI创始人之一、特斯拉前AI总监）最
- Created `wiki/sources/OpenSpec-要补的是-AI-编程之前的-planning-layer让关键决策不再只活在聊天记录里而是变成可追踪的工件系统从-Vibe-Codin.md` from douyin raw transcription: OpenSpec 要补的，是 AI 编程之前的 planning layer，让关键决策不再只活在聊天记录里，而是变成可
- Created `wiki/sources/给-Agent-加记忆前-先想清楚这四个问题-研究了一圈-Agent-Memory-框架后的心得选框架之前先搞清楚记给谁记什么记多久怎么取大部分场景其.md` from douyin raw transcription: 给 Agent 加记忆前 先想清楚这四个问题 研究了一圈 Agent Memory 框架后的心得：选框架之前先搞清楚记给
- Created `wiki/sources/你觉得现在绝密航天有人类么-三角洲行动-我要成为三角洲高手-三角洲s8蝶变时刻新赛季-假期结束接着洲-善战行动.md` from douyin raw transcription: 你觉得现在绝密航天有人类么？ #三角洲行动 #我要成为三角洲高手 #三角洲s8蝶变时刻新赛季 #假期结束接着洲 #善战行
- Created `wiki/sources/5分钟解锁小龙虾Skill全攻略什么是Skill有哪些好用-skill如何安装小白必看进化指南openclaw-skill-ai-前沿科技趋势.md` from douyin raw transcription: 5分钟解锁小龙虾Skill全攻略：什么是Skill？有哪些好用 skill？如何安装？小白必看进化指南！#opencla
- Created `wiki/sources/没有了执着-就有了自由巴沙尔-音乐分享.md` from douyin raw transcription: 没有了执着 就有了自由！#巴沙尔 #音乐分享
- Created `wiki/sources/OpenClaw多Agent共用记忆这个方法太香了-OpenClaw-AI助手-Agent-多Agent-人工智能.md` from douyin raw transcription: OpenClaw多Agent共用记忆，这个方法太香了！ #OpenClaw  #AI助手  #Agent   #多Age
- Created `wiki/sources/为什么AI越强你越需要亲手设计工作流-这两天看了Anthropic的一篇文章Building-effective-agents.md` from douyin raw transcription: 为什么AI越强，你越需要亲手设计工作流？ 这两天看了Anthropic的一篇文章，《Building effective
- Created `wiki/sources/这应该是最全面的Claude-Code源码分析了人工智能-互联网大厂-chatgpt应用领域-AI-编程.md` from douyin raw transcription: 这应该是最全面的Claude Code源码分析了！#人工智能  #互联网大厂 #chatgpt应用领域 #AI #编程
- Created `wiki/sources/上下文腐烂-Context-rot-其实是两种病-大家都在抱怨-agent-越改越烂开一个新对话就一次改对了-这件事过去半年被反复说叫-conte.md` from douyin raw transcription: 上下文腐烂 (Context rot) 其实是两种病 大家都在抱怨 agent 越改越烂、开一个新对话就一次改对了 ——
- Created `wiki/sources/笔记本会自我进化-拥有一个会自我进化的笔记本知识科普-知识分享-AI-AI知识库-笔记.md` from douyin raw transcription: 笔记本会自我进化 拥有一个会自我进化的笔记本#知识科普 #知识分享 #AI #AI知识库 #笔记
- Created `wiki/sources/Hermes-装上这5个skills-直接起飞-Hermes-科技-ai-模型.md` from douyin raw transcription: Hermes 装上这5个skills ，直接起飞！ #Hermes  #科技 #ai #模型
- Created `wiki/sources/untitled.md` from douyin raw transcription: 
- Created `wiki/sources/搞懂Agent三大核心概念-agent-ai新星计划-ai.md` from douyin raw transcription: 搞懂Agent三大核心概念 #agent #ai新星计划 #ai

## 2026-05-25 消化——概念/实体/问题/综合

- Created `wiki/concepts/agent-skill.md` — Agent Skill 概念页.
- Created `wiki/entities/openclaw.md` — OpenClaw 实体页.
- Created `wiki/entities/claude-code.md` — Claude Code 实体页.
- Created `wiki/questions/agent-skill-vs-mcp.md` — Agent Skill vs MCP 问题页.
- Created `wiki/syntheses/ai-knowledge-map.md` — AI 知识库全景图综合页.
- Updated `index.md` with all 5 new pages.

## 2026-05-28 导入 Anthropic 官方 Agent 工程资料

- 调研 Anthropic 官方 Engineering、Newsroom 和 Claude Code 官方文档入口。
- 新增 10 个官方来源记录：`raw/sources/2026-05-28-anthropic-*.source.md`。
- 新增综合页：`wiki/syntheses/anthropic-agent-engineering-map.md`，用于组织 Anthropic Agent、Claude Code、MCP、Agent Skills、上下文工程、多 Agent 和长任务 harness 的官方学习路径。
- 更新 `index.md`、`llms.txt`、`wiki/syntheses/README.md`，把 Anthropic 官方学习地图接入人和 AI 的导航入口。
- 已验证新增官方 URL 返回 200，并检查新增学习地图的本地 Markdown 链接。
