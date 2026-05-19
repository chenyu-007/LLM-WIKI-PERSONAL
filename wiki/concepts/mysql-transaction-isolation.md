---
title: MySQL 事务隔离级别
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/13-mysql-transaction-isolation.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://dev.mysql.com/doc/refman/8.4/en/innodb-transaction-isolation-levels.html
  - https://dev.mysql.com/doc/refman/8.4/en/set-transaction.html
---

# MySQL 事务隔离级别

## 一句话说明

MySQL InnoDB 的事务隔离级别决定一个事务在并发读写中能看到哪些数据，以及读写操作会使用哪些锁和快照规则。

## 要点

- 事务把一组操作作为逻辑单元提交或回滚。
- MySQL InnoDB 支持 Read Uncommitted、Read Committed、Repeatable Read、Serializable。
- InnoDB 默认隔离级别是 Repeatable Read，不是 Read Committed。
- 普通一致性读依赖 [MVCC](mvcc.md) read view。
- 锁定读、`UPDATE`、`DELETE` 等当前读会涉及记录锁、间隙锁或 next-key locks，不能和普通快照读混为一谈。
- 设置隔离级别时应使用 `SET SESSION TRANSACTION ISOLATION LEVEL ...`，注意 `ISOLATION` 拼写。

## 四个级别

- Read Uncommitted：可能读到其他事务未提交的数据，通常很少用于业务系统。
- Read Committed：每次一致性读通常读取该语句开始时可见的已提交版本。
- Repeatable Read：同一事务内普通一致性读通常保持同一 read view，是 InnoDB 默认级别。
- Serializable：更强隔离，通常通过更保守的锁策略降低并发度。

## 关联页面

- [MVCC](mvcc.md)
- [GORM 事务](gorm-transaction.md)
- [为什么 MySQL Repeatable Read 不等于简单快照隔离](../questions/why-mysql-repeatable-read-is-not-the-same-as-snapshot-isolation.md)
- [MySQL EXPLAIN](mysql-explain.md)

## 待核实

- 具体锁行为与 SQL 形态、索引命中情况和 MySQL 版本有关，分析线上问题时要结合实际执行计划和事务日志。
