---
title: OpenFaaS 函数调用路径怎么理解
type: question
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/02-openfaas-gateway-request-chain.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://docs.openfaas.com/architecture/gateway/
  - https://docs.openfaas.com/architecture/invocations/
  - https://docs.openfaas.com/reference/async/
---

# OpenFaaS 函数调用路径怎么理解

## 一句话说明

OpenFaaS 函数调用可以先按“客户端 -> Gateway -> provider / 函数实例 -> 响应或异步结果”这条主线理解。

## 同步调用

```text
Client
  ↓
Gateway /function/
  ↓
provider 查找或转发
  ↓
function instance
  ↓
Gateway 返回响应
```

同步调用适合请求耗时较短、调用方需要立即拿到结果的场景。

## 异步调用

```text
Client
  ↓
Gateway /async-function
  ↓
queue / async worker
  ↓
function instance
  ↓
callback 或日志/指标观察结果
```

异步调用适合耗时任务、削峰或调用方不需要同步等待结果的场景。

## 排查问题时看哪里

- 请求是否到达 [OpenFaaS Gateway](../concepts/openfaas-gateway.md)。
- 函数是否存在，副本数是否为 0，是否触发自动伸缩。
- provider 是否能找到后端函数实例。
- 函数容器日志和指标是否显示执行成功。
- 如果在 kind 本地部署，还要检查端口映射和 Service 暴露方式。

## 关联页面

- [OpenFaaS Gateway](../concepts/openfaas-gateway.md)
- [kind 本地如何暴露 OpenFaaS Gateway](how-kind-exposes-openfaas-gateway-locally.md)
- [Kubernetes Namespace](../concepts/kubernetes-namespace.md)

## 待核实

- 具体中间件、源码函数名和调用栈要按 OpenFaaS 目标版本源码确认。
