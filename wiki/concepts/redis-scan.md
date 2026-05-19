---
title: Redis SCAN
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/15-redis-basics.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://redis.io/docs/latest/commands/scan/
---

# Redis SCAN

## 一句话说明

`SCAN` 是 Redis 的增量迭代命令，用 cursor 分批遍历 keyspace，避免像 `KEYS` 那样一次性阻塞扫描。

## 要点

- `SCAN` 每次返回新的 cursor 和一批 key。
- cursor 回到 `0` 表示一轮遍历结束。
- `COUNT` 是提示值，不是精确返回数量保证。
- `MATCH` 可按 pattern 过滤返回结果，但不等于数据库索引查询。
- 遍历期间 keyspace 变化时，结果可能重复或遗漏，调用方要能容忍。

## 适用范围

适合：

- 运维巡检、低频后台任务、渐进式清理。
- 查找某类 key 的候选集合。

不适合：

- 在线请求路径中频繁全库遍历。
- 依赖一次遍历得到强一致快照。

## 关联页面

- [Redis 数据类型](redis-data-types.md)
- [Redis 大 key 删除](redis-big-key-deletion.md)
- [Redis ACL](redis-acl.md)

## 待核实

- 大规模实例执行扫描任务前，需要结合实例负载、key 数量和业务低峰窗口压测。
