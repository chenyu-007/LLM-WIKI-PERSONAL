---
title: Redis ACL
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/15-redis-basics.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://redis.io/docs/latest/operate/oss_and_stack/management/security/acl/
---

# Redis ACL

## 一句话说明

Redis ACL 用用户、命令权限和 key pattern 控制客户端能执行什么操作、访问哪些 key。

## 要点

- Redis 6 起提供更细粒度的 ACL 能力。
- ACL 可以限制用户可执行命令、可访问 key 范围和认证方式。
- ACL 是最小权限控制的一部分，不替代网络隔离、TLS、审计和配置安全。
- 旧版本 Redis 主要依赖全局密码等较粗粒度控制。

## 适用范围

适合：

- 多应用共享 Redis 时降低误操作面。
- 限制只读客户端、运维客户端和业务客户端的权限。
- 保护关键 key pattern。

不适合：

- 把 Redis 暴露到不可信网络后只靠 ACL 防护。
- 替代业务层权限校验。

## 关联页面

- [Redis 数据类型](redis-data-types.md)
- [Redis SCAN](redis-scan.md)

## 待核实

- ACL 语法和推荐配置要以目标 Redis 版本官方文档为准。
