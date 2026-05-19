---
title: SQL 索引设计
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/12-mysql-sql-tuning.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://dev.mysql.com/doc/refman/8.4/en/optimization-indexes.html
---

# SQL 索引设计

## 一句话说明

SQL 索引设计是在读写成本之间做权衡，让高频查询能更少扫描、更少排序、更少回表。

## 要点

- 索引优先服务高频、慢、业务关键的查询，不是越多越好。
- 常见候选列来自 `WHERE`、`JOIN`、`ORDER BY`、`GROUP BY`。
- 联合索引要考虑列顺序、选择性、范围条件和排序需求。
- 在索引列上包函数、隐式类型转换或前导通配符，可能让索引难以利用。
- `SELECT *` 会增加读取和网络传输成本，也可能破坏覆盖索引机会。
- N+1 查询、大 `IN` 列表和无边界分页都可能比单个索引问题更严重。

## 常见判断

- 过滤条件稳定且选择性高，通常更值得考虑索引。
- 只为低选择性字段单独建索引，收益可能有限。
- 排序和分组能否利用索引，取决于查询条件、索引顺序和优化器判断。
- 写入频繁的表需要控制索引数量，因为索引会增加写放大。

## 关联页面

- [MySQL EXPLAIN](mysql-explain.md)
- [如何诊断 MySQL 慢查询](../questions/how-to-diagnose-a-slow-mysql-query.md)

## 待核实

- 具体索引方案必须结合真实表结构、数据分布、查询频率和 MySQL 版本验证。
