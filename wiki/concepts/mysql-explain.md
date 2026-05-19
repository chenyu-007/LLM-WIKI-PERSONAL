---
title: MySQL EXPLAIN
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/12-mysql-sql-tuning.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://dev.mysql.com/doc/refman/8.4/en/explain-output.html
---

# MySQL EXPLAIN

## 一句话说明

`EXPLAIN` 用来查看 MySQL 优化器为一条语句选择的执行计划，是排查慢 SQL 的第一层入口。

## 要点

- `EXPLAIN` 关注的是优化器计划，不等于完整运行时性能。
- 常看字段包括访问类型、候选索引、实际使用索引、扫描行数、过滤比例和 `Extra`。
- `key` 为空通常说明没有使用索引，但是否需要建索引要结合数据量、选择性和查询频率判断。
- `rows` 是估算值，不是实际扫描行数。
- `Extra` 中的 `Using filesort` 表示需要额外排序步骤，可能在内存或磁盘完成，不等于一定发生磁盘排序。
- `Using temporary` 表示查询可能需要临时表，是性能警告信号，但严重程度取决于数据量、执行计划和配置。

## 调优时怎么用

1. 先用慢查询日志、APM 或监控定位具体 SQL。
2. 用 `EXPLAIN` 看索引、扫描行数和排序/临时表信号。
3. 检查 `WHERE`、`JOIN`、`ORDER BY`、`GROUP BY` 是否有合适索引支撑。
4. 修改索引或 SQL 后重新 `EXPLAIN` 对比计划。
5. 必要时再用 `EXPLAIN ANALYZE` 查看运行时信息。

## 适用范围

适合：

- 判断 SQL 是否使用了预期索引。
- 初步发现全表扫描、低效 join、额外排序和临时表。
- 给 [如何诊断 MySQL 慢查询](../questions/how-to-diagnose-a-slow-mysql-query.md) 提供证据。

不适合：

- 单独证明一条 SQL 的真实耗时。
- 替代线上监控、慢查询日志和业务压测。

## 关联页面

- [SQL 索引设计](sql-indexing.md)
- [如何诊断 MySQL 慢查询](../questions/how-to-diagnose-a-slow-mysql-query.md)
- [MySQL 事务隔离级别](mysql-transaction-isolation.md)

## 待核实

- 不同 MySQL 版本的 `EXPLAIN` 输出字段和优化器行为会变化，引用具体字段时要核对目标版本文档。
