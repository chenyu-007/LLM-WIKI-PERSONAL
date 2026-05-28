---
title: AI Agent
type: concept
status: active
updated: 2026-05-27
sources:
  - wiki/sources/RAG 时代终结编译期知识层来了 RAG AI资讯 Pinecone Agent 前沿科技.md
  - wiki/sources/一个公式讲清Agent长期记忆AI的记笔记比你想象聪明 先看清问题的本质Agent 的长期记忆不是数据库存的是值得记住的.md
  - wiki/sources/搞懂Agent三大核心概念-agent-ai新星计划-ai.md
  - wiki/sources/单体Agent起步拒绝造火箭-单体Agent起步拒绝造火箭AnthropicBuilding-Effective-AI-Agents-Architec.md
  - wiki/sources/Agent的能力上限到底在哪01-大模型应用开发AI应用开发-Anthropic-Agent开发.md
---

# AI Agent

## 是什么

Agent 是能**自主执行任务**的 AI 系统——不只是回答问题，而是感知环境、做决策、调用工具、完成多步骤目标。

## Agent vs Chatbot

| | Chatbot | Agent |
|---|---------|-------|
| 模式 | 一问一答 | 多步骤执行 |
| 记忆 | 当前对话窗口 | 长期记忆 + 上下文管理 |
| 工具 | 无 | MCP 工具、Skill、API |
| 输出 | 文本回复 | 动作（写文件、调接口、发消息） |

## Agent 三大核心

1. **规划 (Planning)** — 拆任务、排顺序、处理异常。
2. **记忆 (Memory)** — 短期（对话上下文）+ 长期（跨会话知识）。
3. **工具 (Tools)** — MCP、API、Skill，扩展 Agent 能力边界。

## Agent 不是聊天

关键区别：Agent 每次执行任务不该从零检索——RAG 给 Chatbot 设计的"搜-读-答"模式跟不上 Agent 的多步执行需求。编译期知识层（Pinecone Nexus）的思路是：提前把知识编译好，Agent 直接拿结构化成品，省掉 85% 的重复检索算力。

## 相关页面

- [Agent Skill](agent-skill.md)
- [Agent Memory](agent-memory.md)
- [Model Context Protocol](model-context-protocol.md)
- [Anthropic](../entities/anthropic.md)
