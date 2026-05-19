---
title: 为什么 MySQL Repeatable Read 不等于简单快照隔离
type: question
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/13-mysql-transaction-isolation.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://dev.mysql.com/doc/refman/8.4/en/innodb-transaction-isolation-levels.html
---

# 为什么 MySQL Repeatable Read 不等于简单快照隔离

## 一句话说明

InnoDB Repeatable Read 下既有基于 read view 的普通一致性读，也有会加锁的当前读和写操作，所以不能简单理解成“所有读都只看事务开始快照”。

## 判断方式

- 普通 `SELECT` 通常是一致性读，使用 [MVCC](../concepts/mvcc.md) read view。
- `SELECT ... FOR UPDATE`、`SELECT ... FOR SHARE` 属于锁定读，读取当前版本并加锁。
- `UPDATE`、`DELETE` 也属于当前读语义，会根据索引和范围加锁。
- 防止幻读的机制要结合 SQL 类型看：普通一致性读靠快照可见性；锁定读和写操作可能使用 next-key locks。

## 为什么容易误解

- 教材常把隔离级别和脏读、不可重复读、幻读简单对应，但实现细节比表格复杂。
- “RR 防幻读”这句话不说明普通读和锁定读区别，容易误导。
- 是否命中索引会影响锁范围，进而影响并发行为。

## 关联页面

- [MySQL 事务隔离级别](../concepts/mysql-transaction-isolation.md)
- [MVCC](../concepts/mvcc.md)
- [MySQL EXPLAIN](../concepts/mysql-explain.md)

## 待核实

- 遇到真实幻读、锁等待或死锁问题时，需要结合表结构、索引、SQL、隔离级别和 `SHOW ENGINE INNODB STATUS` 等信息分析。
