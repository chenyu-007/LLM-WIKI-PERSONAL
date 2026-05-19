---
title: Kubernetes Namespace
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/11-openfaas-kind-kubernetes-namespace.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
  - https://docs.openfaas.com/reference/namespaces/
---

# Kubernetes Namespace

## 一句话说明

Kubernetes Namespace 用来在同一集群内划分资源命名空间，帮助隔离资源名称、访问范围和管理边界。

## 要点

- Namespace 适合在同一集群内划分环境、团队或系统组件。
- Namespace 不是强安全边界，安全还需要 RBAC、NetworkPolicy、准入控制等机制。
- 很多 Kubernetes 资源属于某个 namespace，例如 Pod、Service、Deployment。
- OpenFaaS 常见部署会区分控制平面 namespace 和函数 namespace，例如 `openfaas` 与 `openfaas-fn`。

## 在 OpenFaaS 中的意义

- 控制平面组件放在独立 namespace，便于管理 Gateway、队列、provider 等组件。
- 用户函数放在函数 namespace，便于区分平台组件和业务函数。
- 排查函数访问问题时，要确认资源是否在预期 namespace。

## 关联页面

- [OpenFaaS Gateway](openfaas-gateway.md)
- [kind 本地如何暴露 OpenFaaS Gateway](../questions/how-kind-exposes-openfaas-gateway-locally.md)

## 待核实

- 具体 namespace 名称取决于 OpenFaaS 安装方式和参数，不应把示例名称写成唯一标准。
