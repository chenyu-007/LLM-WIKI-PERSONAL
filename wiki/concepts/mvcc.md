---
title: MVCC
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/13-mysql-transaction-isolation.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://dev.mysql.com/doc/refman/8.4/en/innodb-transaction-isolation-levels.html
---

# MVCC

## 一句话说明

MVCC（Multi-Version Concurrency Control）通过保存数据的多个版本，让读操作在很多情况下不用阻塞写操作。

## 要点

- MVCC 的目标是提升并发读写下的一致性和性能。
- 在 InnoDB 中，普通一致性读会基于 read view 判断哪个版本对当前事务可见。
- MVCC 主要解释的是快照读，不等于所有并发控制。
- 锁定读、写操作和范围更新仍可能需要锁。
- 隔离级别不同，read view 创建和复用方式也不同。

## 常见误区

- 误区：用了 MVCC 就不会有锁。
- 现实：MVCC 优化普通读；写写冲突、锁定读和范围更新仍然涉及锁。
- 误区：Repeatable Read 下所有读都完全一样。
- 现实：普通一致性读和当前读语义不同。

## 关联页面

- [MySQL 事务隔离级别](mysql-transaction-isolation.md)
- [为什么 MySQL Repeatable Read 不等于简单快照隔离](../questions/why-mysql-repeatable-read-is-not-the-same-as-snapshot-isolation.md)

## 待核实

- 如果要解释 undo log、read view 字段和版本链，需要回到 MySQL 目标版本文档或源码资料进一步核对。
