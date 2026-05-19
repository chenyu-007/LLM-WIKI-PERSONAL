---
title: Redis 大 key 删除
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/15-redis-basics.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://redis.io/docs/latest/commands/unlink/
---

# Redis 大 key 删除

## 一句话说明

删除大 key 可能阻塞 Redis 主线程，`UNLINK` 可以把内存释放放到后台异步处理，降低阻塞风险。

## 要点

- `DEL` 会同步删除 key，释放大对象时可能带来明显延迟。
- `UNLINK` 会先从 keyspace 移除 key，再异步释放内存。
- `UNLINK` 不是容量规划的替代品，大 key 本身仍会影响网络、复制、持久化和延迟。
- 清理大 key 前应先识别类型、大小、访问频率和业务归属。

## 常见做法

- 用扫描任务找候选 key，不在高峰期全库遍历。
- 对大集合类 key 优先考虑分片、分桶或生命周期设计。
- 删除前确认业务不再依赖该 key。
- 批量清理时控制速率，观察延迟和内存变化。

## 关联页面

- [Redis 数据类型](redis-data-types.md)
- [Redis SCAN](redis-scan.md)
- [Redis 持久化](redis-persistence.md)

## 待核实

- lazy freeing 行为和后台线程配置需要结合目标 Redis 版本和实例配置确认。
