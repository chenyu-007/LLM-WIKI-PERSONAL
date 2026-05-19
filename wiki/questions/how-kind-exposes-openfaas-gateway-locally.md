---
title: kind 本地如何暴露 OpenFaaS Gateway
type: question
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/11-openfaas-kind-kubernetes-namespace.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://kind.sigs.k8s.io/docs/user/configuration/
---

# kind 本地如何暴露 OpenFaaS Gateway

## 一句话说明

kind 可以通过 `extraPortMappings` 把宿主机端口映射到 kind 节点端口，再由 Kubernetes Service 转发到 OpenFaaS Gateway。

## 典型链路

```text
宿主机 localhost:端口
  ↓
kind 节点端口映射
  ↓
Kubernetes NodePort / Service
  ↓
OpenFaaS Gateway Pod
```

## 关键判断

- kind 的端口映射配置只负责宿主机到 kind 节点。
- Kubernetes Service 负责把节点端口或集群内地址转发到 Pod。
- OpenFaaS Gateway 自身仍运行在某个 namespace 中。
- 示例端口不是标准，必须看当前 kind 配置和 Service 配置。

## 关联页面

- [OpenFaaS Gateway](../concepts/openfaas-gateway.md)
- [Kubernetes Namespace](../concepts/kubernetes-namespace.md)
- [OpenFaaS 函数调用路径怎么理解](openfaas-function-invocation-path.md)

## 待核实

- 具体端口、Service 类型和 namespace 要以本地集群配置为准。
