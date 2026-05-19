---
title: GORM 事务
type: concept
status: active
updated: 2026-05-16
sources:
  - raw/inbox/youdao/approved-2026-05-15/13-mysql-transaction-isolation.md
  - raw/inbox/youdao/approved-2026-05-15/review.md
  - https://gorm.io/docs/transactions.html
---

# GORM 事务

## 一句话说明

GORM 提供 `Transaction`、手动事务、nested transaction、SavePoint 和 RollbackTo 等事务控制方式。

## 要点

- 推荐优先使用 `db.Transaction(func(tx *gorm.DB) error { ... })`，由 GORM 根据返回错误提交或回滚。
- 手动事务适合需要精细控制 begin、commit、rollback 的场景。
- GORM 官方文档包含 nested transaction 示例，不应写成“默认不支持嵌套事务”。
- SavePoint 和 RollbackTo 可以用于局部回滚，但会增加控制流复杂度。
- ORM 事务只负责应用层调用方式，底层隔离语义仍由数据库和连接配置决定。

## 使用边界

适合：

- 把多次数据库写入包成一个原子业务动作。
- 在服务层明确提交/回滚边界。
- 需要局部回滚时使用 SavePoint。

不适合：

- 用长事务包住外部 API、文件 IO 或用户交互。
- 把 ORM 的事务封装当成隔离级别本身。

## 关联页面

- [MySQL 事务隔离级别](mysql-transaction-isolation.md)
- [MVCC](mvcc.md)

## 待核实

- 具体代码示例需要结合项目当前 GORM 版本、数据库驱动和连接池配置验证。
