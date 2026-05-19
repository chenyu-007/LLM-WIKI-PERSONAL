---
title: Redis 数据类型
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/15-redis-basics.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://redis.io/docs/latest/develop/data-types/
---

# Redis 数据类型

## 一句话说明

Redis 是数据结构服务器，一个 key 对应一个带类型的 value，不是关系型数据库里的表、行、列模型。

## 要点

- 常见类型包括 String、Hash、List、Set、Sorted Set、Stream、Bitmap、HyperLogLog 等。
- String 是二进制安全的字节序列，可用于缓存值、计数器、分布式锁 token、位图等。
- Hash 适合存对象字段，但不等于关系型表。
- List 适合按插入顺序处理元素，内部实现随 Redis 版本演进，不能固定写成某一种结构。
- Sorted Set 通过 score 维护有序集合，适合排行榜、延迟队列候选、范围查询等场景。
- 对已存在的 key 使用不匹配类型的命令通常会返回 WRONGTYPE，而不是自动把类型改掉。

## 类型变更规则

- `SET key value` 可以把一个 key 覆盖成 String 类型。
- 已存在 String key 时执行 `HSET key field value` 通常会报 WRONGTYPE。
- 要改变 key 的数据类型，应先删除旧 key、选择新 key，或使用明确会覆盖的命令语义。

## 关联页面

- [Redis 持久化](redis-persistence.md)
- [Redis ACL](redis-acl.md)
- [Redis SCAN](redis-scan.md)
- [Redis 大 key 删除](redis-big-key-deletion.md)

## 待核实

- 内部编码和底层结构会随 Redis 版本变化。除非讨论源码或性能细节，否则页面只记录稳定的用户可见语义。
