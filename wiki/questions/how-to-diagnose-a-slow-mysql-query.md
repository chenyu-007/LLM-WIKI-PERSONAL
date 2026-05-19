---
title: 如何诊断 MySQL 慢查询
type: question
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/12-mysql-sql-tuning.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://dev.mysql.com/doc/refman/8.4/en/explain-output.html
---

# 如何诊断 MySQL 慢查询

## 一句话说明

慢查询诊断要先定位真实慢 SQL，再用执行计划、索引、数据量和业务访问模式逐层排查。

## 判断流程

1. 从慢查询日志、APM、数据库监控或业务日志定位具体 SQL。
2. 确认慢是偶发还是稳定复现，排除锁等待、网络抖动和实例负载尖峰。
3. 用 [MySQL EXPLAIN](../concepts/mysql-explain.md) 看访问类型、索引、扫描行数和 `Extra`。
4. 对照 [SQL 索引设计](../concepts/sql-indexing.md) 检查过滤、连接、排序和分组条件。
5. 检查是否存在 N+1 查询、大分页、大 `IN`、无必要字段读取或应用层重复查询。
6. 修改后用相同数据量和相同条件复测，不只看语法是否正确。

## 常见结论

- 没用索引不一定就是错，表很小或选择性很低时优化器可能故意不用。
- 用了索引也不一定快，回表多、排序多、临时表大或返回行数太多仍会慢。
- `Using filesort` 和 `Using temporary` 是警告信号，不是自动判死刑。
- 调优目标不是让 `EXPLAIN` 看起来漂亮，而是降低实际业务延迟和资源消耗。

## 关联页面

- [MySQL EXPLAIN](../concepts/mysql-explain.md)
- [SQL 索引设计](../concepts/sql-indexing.md)

## 待核实

- 如果慢查询涉及事务锁、隔离级别或死锁，需要结合 [MySQL 事务隔离级别](../concepts/mysql-transaction-isolation.md) 进一步分析。
