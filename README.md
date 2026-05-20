# LLM Wiki

这是一个按 Karpathy 原始模式搭建的本地 LLM Wiki。它的目标不是把所有资料丢给向量库，而是先把资料整理成一层人和 AI 都能直接阅读、链接、维护的 Markdown 知识层。

## 为什么这样搭建

传统知识库通常面向人：目录、长文、搜索框足够使用。但 LLM 需要更稳定的上下文边界、来源引用、短页面、交叉链接和维护规约。LLM Wiki 把知识库拆成三层：

1. `raw/` 保存原始资料和来源记录，承担事实依据。
2. `wiki/` 保存整理后的知识页面，承担查询、推理和复用。
3. `AGENTS.md`、`schema/`、`templates/` 约束 AI 如何维护这套知识。

这样做的好处是：人可以正常浏览 Markdown，AI 也能按规则读取、更新、追溯和纠错。

## 当前结构

```text
llm-wiki/
  AGENTS.md
  README.md
  index.md
  log.md
  llms.txt
  raw/
  schema/
  templates/
  wiki/
```

## 最小使用方式

### 1. 放入原始资料

把 PDF、网页链接、会议纪要、项目文档或手工摘录放到 `raw/`。如果只是网页来源，先建立一个 `.source.md` 来源记录。

### 2. 编写 Wiki 页面

把原始资料整理成 `wiki/` 下的小页面。每个页面只讲一个概念、实体、问题或来源总结。

### 3. 更新索引

把重要页面加入 `index.md`，让人和 AI 都能从入口页找到它。

### 4. 记录日志

每次导入、重构或纠错，在 `log.md` 追加记录。

### 5. 推送到 GitHub

每次更新知识库后，完成链接和结构检查，再提交并 `git push` 到远程仓库。

## HTML 阅读层

本 Wiki 的唯一知识源仍然是 Markdown。为了方便人阅读，可以使用旁路 Quartz 工程 `../llm-wiki-site/` 把当前 Markdown 自动构建成 HTML。

阅读层不手工维护内容：

- 在 `llm-wiki/` 中维护 `raw/`、`wiki/`、`index.md` 和 `log.md`。
- 在 `llm-wiki-site/` 中运行 `npm run build:wiki` 生成 HTML。
- 生成物位于 `llm-wiki-site/public/`，可以随时删除并重新构建。

## 什么时候再升级

当前版本先不用向量库、知识图谱或 MCP。等页面数量明显增多，或者出现跨目录检索慢、权限复杂、多人并发维护的问题，再考虑增加：

- 全文检索或向量检索。
- `lint` 脚本。
- MCP server。
- 自动生成 `llms-full.txt` 的导出流程。
