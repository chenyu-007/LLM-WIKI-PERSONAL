---
title: Redis 持久化
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/15-redis-basics.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://redis.io/docs/latest/operate/oss_and_stack/management/persistence/
---

# Redis 持久化

## 一句话说明

Redis 是否重启丢数据取决于持久化配置和故障时机，不能简单说“默认一定丢”或“一定不丢”。

## 要点

- Redis 主要持久化方式包括 RDB、AOF，以及两者组合使用。
- RDB 是按时间点生成快照，恢复快，但可能丢失最近一次快照后的写入。
- AOF 记录写命令，通常能降低数据丢失窗口，但文件更大，恢复和重写有额外成本。
- 关闭持久化时，Redis 更像纯内存缓存，重启后数据不可依赖。
- 生产环境要按业务容忍的数据丢失窗口和恢复时间目标配置。

## 设计判断

- 纯缓存：可以接受丢失，重点是回源能力和缓存预热。
- 会话、队列、计数等重要数据：要明确持久化、复制、备份和故障恢复策略。
- 金融账务等强一致场景：通常不应只靠 Redis 持久化承载最终事实。

## 关联页面

- [Redis 数据类型](redis-data-types.md)
- [Redis 大 key 删除](redis-big-key-deletion.md)

## 待核实

- Redis 发行版、部署方式和配置模板可能不同，判断“默认是否开启某种持久化”必须看当前实例配置。
