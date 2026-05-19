---
title: OpenFaaS Gateway
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/02-openfaas-gateway-request-chain.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://docs.openfaas.com/architecture/gateway/
  - https://docs.openfaas.com/architecture/invocations/
  - https://docs.openfaas.com/reference/async/
  - https://docs.openfaas.com/architecture/autoscaling/
---

# OpenFaaS Gateway

## 一句话说明

OpenFaaS Gateway 是 OpenFaaS 的入口组件，负责函数调用、管理 API、UI/Portal、指标和与 provider 的协作。

## 要点

- 同步函数调用通常通过 `/function/` 路由进入。
- 异步调用通过 `/async-function` 进入，并由异步队列和相关组件处理。
- Gateway 不直接等同于函数运行时；函数实例通常运行在 Kubernetes 等后端平台上。
- Gateway 可以参与函数调用统计和自动伸缩决策。
- OpenFaaS 自动伸缩使用官方定义的函数标签，例如 `com.openfaas.scale.type`、`com.openfaas.scale.target`、`com.openfaas.scale.min`、`com.openfaas.scale.max`。

## 不写成确定结论的内容

- 原笔记中的具体函数名、源码路径和 `singleflight` 等实现细节属于某个源码版本，需要按目标仓库版本校验后才能写入源码阅读页。
- `com.openfaas.memory-size`、`com.openfaas.cold-start-cost` 不作为 OpenFaaS 官方标签记录。

## 关联页面

- [OpenFaaS 函数调用路径怎么理解](../questions/openfaas-function-invocation-path.md)
- [Kubernetes Namespace](kubernetes-namespace.md)
- [kind 本地如何暴露 OpenFaaS Gateway](../questions/how-kind-exposes-openfaas-gateway-locally.md)

## 待核实

- 若后续要分析具体源码链路，需要锁定 OpenFaaS 版本和仓库 commit。
