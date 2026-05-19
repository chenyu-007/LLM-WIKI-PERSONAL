---
source: youdao-note
youdao_id: WEB5108b46d072d9fc3757051f15514487a
title: 事务&&隔离级别.note
captured: 2026-05-15
status: pending-review
---

事务
事务（Transaction）是数据库操作的逻辑单元，可以包含一组 SQL 语句。
它的核心特点是：
要么全部成功，要么全部失败。比如转账操作：
A 账户扣款 100 元
B 账户增加 100 元
这两个操作必须同时成功或同时失败，否则会导致数据不一致。
事务的四大特性（ACID）
特性 说明 生活化例子 原子性(Atomicity) 事务中的操作要么全部完成，要么全部不执行。（没有中间状态） 网购付款：要么支付成功（扣钱+发货），要么支付失败（钱退回+不发货）。 一致性(Consistency) 事务执行前后，数据库的数据必须满足所有业务规则。（比如 age INT CHECK (age >= 0) ） 绝对不能插入-1的数据 隔离性(Isolation) 多个并发事务之间互不干扰，如同串行执行。 多人同时抢票，系统保证不会重复卖同一张票。 持久性(Durability) 事务提交后，对数据的修改永久保存（即使系统崩溃）。 银行转账成功后，数据立即写入硬盘，断电也不丢失。
原子性（A）：事务内部的操作，要么全做要么全不做。
一致性（C）：事务执行前后，整个数据库必须满足约束规则。
CREATE TABLE users (  id INT PRIMARY KEY,  name VARCHAR(50) NOT NULL,  age INT CHECK (age >= 0));
这个表有几个约束：
主键不能重复
name 不能为空
age 必须 ≥ 0
❌ 示例：违反一致性但原子性没错
BEGIN;INSERT INTO users (id, name, age) VALUES (1, 'Alice', -5); -- ❌ age 不合法COMMIT;
这条语句虽然是“原子的”（一次性失败了，没有插入任何数据）
但它违反了 age ≥ 0 的一致性规则
所以：原子性 OK，一致性被数据库自己强行保障住了（执行失败）
怎么使用事务？
MySQL 中使用事务？
（1）显式控制事务
-- 1. 开启事务START TRANSACTION;  -- 或 BEGIN;-- 2. 执行一组 SQL 操作UPDATE account SET balance = balance - 100 WHERE id = 1;  -- A 账户扣款UPDATE account SET balance = balance + 100 WHERE id = 2;  -- B 账户收款-- 3. 提交或回滚COMMIT;   -- 确认全部成功-- 或ROLLBACK; -- 撤销所有操作（比如执行出错时）
（2）自动提交模式
默认情况下，MySQL 每条 SQL 都会自动提交（即每条 SQL 都是一个独立事务）。
关闭自动提交：
SET autocommit = 0;  -- 关闭自动提交-- 执行多条 SQL 后手动提交或回滚COMMIT;
GORM 中使用事务？
在 GORM 中使用事务（Transaction）非常简单，有两种主流方式，分别适用于不同场景：
db.Transaction(func(tx *gorm.DB) error)
这是推荐写法，由 GORM 自动开始、提交或回滚事务：
            err := db.Transaction(func(tx *gorm.DB) error {    	    // 在 tx 上进行所有数据库操作	    if err := tx.Create(&User{Name: "Alice"}).Error; err != nil {		return err // 返回 error 会触发 rollback	    }            if err := tx.Create(&User{Name: "Bob"}).Error; err != nil {		return err // rollback	    }	    // 返回 nil 会 commit	    return nil            })          if err != nil {	      fmt.Println("事务失败，已回滚:", err)          }
✅ 优点
自动管理 begin/commit/rollback，写法简洁
panic 会自动 rollback
不需要你手动判断每一步都成功与否，统一返回 error 即可
手动管理事务
适合更复杂或有多个 return 分支的情况：
tx := db.Begin() // 显式开启事务// 步骤1    if err := tx.Create(&User{Name: "Alice"}).Error; err != nil {	  tx.Rollback()          return err    }// 步骤2    if err := tx.Create(&User{Name: "Bob"}).Error; err != nil {	 tx.Rollback()	 return err    }    if err := tx.Commit().Error; err != nil {	 return err    }
⚠️ 注意：
每一步操作都必须检查 err
如果中间出错，需要 tx.Rollback()
最后一定要记得 tx.Commit() 或 Rollback()
常见错误
1. ❌ 错误使用原始 db 而非 tx
tx := db.Begin()db.Create(&User{Name: "Alice"}) // ❌ 错了，没用 txtx.Commit()
你应该这样写：
tx.Create(&User{Name: "Alice"}) // ✅ 正确
2. ⛔ 不支持嵌套事务
GORM 默认不支持嵌套事务，调用两次 db.Transaction 并不会产生真正的嵌套事务。如果你需要，可以模拟嵌套（SavePoint / RollbackTo），但一般不建议那样做。
场景 推荐用法 逻辑较简单、推荐写法 db.Transaction(func(tx *gorm.DB) error) 多个分支，控制更灵活 手动 .Begin()/.Commit()/.Rollback()
事务的隔离级别
三种数据不一致
当多个事务同时对数据库进行读写操作时，如果没有有效的隔离机制，就会引发一些经典的数据不一致问题。主要有以下三种：
1. 脏读 (Dirty Read)
定义: 一个事务（A）读取到了另一个未提交事务（B）所做的修改。如果事务B最终回滚了，那么事务A读取到的就是“脏”的、根本不存在的数据。
2. 不可重复读 (Non-Repeatable Read)
定义: 在同一个事务内，两次执行相同的查询，返回的结果集却不一样。这是因为在两次查询之间，有另一个事务（B）提交了对这些数据的修改（UPDATE）或删除（DELETE）。
3. 幻读 (Phantom Read)
定义: 在同一个事务内，两次执行相同的范围查询，第二次查询返回了第一次查询中多了不存在的新行(数据行数增多)。
这是因为在两次查询之间，有另一个事务（B）提交了插入（INSERT）操作。
不可重复读：侧重于修改和删除。是同一条数据的内容，在两次读取之间发生了变化。
幻读：侧重于“新增”。是一批数据的行数，在两次读取之间发生了变化，多出了一些“幻影”般的记录。
四种隔离级别
为了解决上述问题，SQL标准定义了四种隔离级别，隔离性从低到高，但并发性能通常从高到低。
隔离级别 (Isolation Level) 脏读 (Dirty Read) 不可重复读 (Non-Repeatable Read) 幻读 (Phantom Read) 1. 读未提交 (Read Uncommitted) 可能 可能 可能 2. 读已提交 (Read Committed) 解决 可能 可能 3. 可重复读 (Repeatable Read) 解决 解决 可能 4. 串行化 (Serializable) 解决 解决 解决
1. 读未提交 (Read Uncommitted)
隔离性最低: 一个事务可以读取到其他事务未提交的修改。
解决了什么问题: 什么都没解决，它允许所有并发问题发生。
实现方式: 基本不加锁，或者说锁的粒度非常小、时间非常短。
应用场景: 几乎不用。只在那些对数据一致性要求极低，但对性能要求极高的场景下，可能会考虑（比如对某个大表的行数进行不精确的实时统计）。
2. 读已提交 (Read Committed)
 解决了脏读。
定义: 一个事务只能读取到其他事务已经提交的数据。
实现方式: 通常通过**MVCC（多版本并发控制）**实现。当一个事务开始读取时，已经被提交的数据库“快照”。不过此处快照是“实时快照”模式，事务里每次select都会更新一次快照，这就会导致不同的select可能会看到不同的结果
仍存在的问题: 不可重复读、幻读。因为在同一个事务的执行过程中，其他事务可能会提交新的修改，所以两次查询的结果可能不同。
应用场景: 主流数据库的默认隔离级别。
3. 可重复读 (Repeatable Read)
解决了脏读和不可重复读。
定义: 在一个事务开始时，它就“锁定”了它所读取的数据的版本。在整个事务执行期间，无论其他事务如何修改并提交，它多次读取同一份数据，结果都是一样的。
实现方式: 同样基于MVCC。它创建的“快照”是在事务开始时的那一刻，并且在整个事务期间都使用这个快照。select也不会改变，这个“一次性快照”保证了你已有的数据行不会变，但它无法阻止别人插入新的数据行。
仍存在的问题: 幻读。它保证了你读取的已有行不会变，但无法阻止其他事务插入新行。所以，范围查询的行数可能会变。
MySQL InnoDB的特殊情况: InnoDB引擎在可重复读这个级别下，通过**间隙锁（Gap Lock）和临键锁（Next-Key Lock）**等机制，在很大程度上也解决了幻读问题。所以MySQL的默认隔离级别（可重复读）实际上比标准定义更强大。MVCC无法阻止其他事务INSERT新的、你从未见过的行。间隙锁是一种锁定索引记录之间“间隙”的锁，它不锁定记录本身，只锁定记录与记录之间的空隙。它的作用是阻止其他事务在这个“间隙”中插入 (INSERT) 新的记录。但这个操作解决幻读本质还是SELECT ... FOR UPDATE（这个才会触发间隙锁，普通的select根本就做不到触发这个间隙锁）
应用场景: MySQL InnoDB引擎的默认隔离级别。提供了很高的数据一致性保证。
视角一：对于“快照读” (普通 SELECT)
它如何解决幻读？ 通过MVCC。
解决方法: 它让你*看不见”幻读。在你的事务开始时，它给你拍了一张“照片”（Read View）。之后无论其他事务插入多少新数据，你反复看这张“照片”，上面的内容（行数）永远不会变。
局限性: 这是一种“鸵鸟策略”。你只是看不到幻影，但幻影（新插入的行）在数据库的“真实世界”里是客观存在的。
这会产生一个问题：如果你接下来的业务逻辑，依赖于你“看到”的这个结果，并试图去修改数据，就会出问题。
视角二：对于“当前读” (SELECT ... FOR UPDATE)
它如何解决幻读？通过锁 (临键锁/间隙锁)。
解决方法: 它让你**“阻止”**幻读的发生。当你执行SELECT ... FOR UPDATE时，你不再是看“照片”了，而是直接走到了“现实世界”里，并且大喊一声：“这个地方我看上了，在我走之前，谁也别在这儿盖房子（INSERT）！”
机制: 它通过间隙锁和临键锁，将你查询的范围（包括存在的记录和不存在的间隙）全部锁定。
4. 串行化 (Serializable)
解决了什么问题: 解决了所有问题（脏读、不可重复读、幻读）。
隔离性最高: 强制所有事务串行执行，一个接一个地排队。
实现方式: 通常通过对所有读取和写入的数据加锁来实现。当一个事务在操作一张表时，其他事务必须等待。
仍存在的问题: 没有并发问题了，但带来了严重的性能问题。并发度几乎为零。
应用场景: 只在那些对数据一致性要求极其严格，且可以接受牺牲并发性能的场景下使用，比如涉及银行关键账目或库存的、不允许任何偏差的操作。
你可以这样来记忆：
读未提交: “毫无底线”，什么都可能发生。
读已提交: 解决了脏读，保证你读到的都是“干净”的、已提交的数据。（主流选择）
可重复读: 在“读已提交”的基础上，又解决了不可重复读，保证你反复读，结果都一样。（MySQL默认）
串行化: 在“可重复读”的基础上，又解决了幻读，保证绝对的数据一致性，但牺牲了并发。（性能杀手）设置隔离级别： 
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;
设置隔离级别的两种方式
1. 临时设置（当前会话或全局）
设置当前会话的隔离级别（仅影响当前连接）：SET SESSION TRANSACTION ISOLATION LEVEL <隔离级别>;-- 示例：设置为读已提交SET SESSION TRANSACTION ISLATION LEVEL READ COMMITTED;设置全局隔离级别（影响后续所有新连接，需权限）：SET GLOBAL TRANSACTION ISOLATION LEVEL <隔离级别>;-- 示例：设置为可重复读SET GLOBAL TRANSACTION ISOLATION LEVEL REPEATABLE READ;
2. 通过配置文件永久生效
修改 MySQL 配置文件（my.cnf 或 my.ini），在 [mysqld] 部分添加：
[mysqld]transaction-isolation = <隔离级别>-- 示例：transaction-isolation = READ-COMMITTED
注意事项
存储引擎支持：只有 InnoDB 等支持事务的引擎可用，MyISAM 不支持。
避免长事务：长时间未提交的事务会占用资源，可能导致死锁。
合理选择隔离级别：隔离级别越高，并发性能越低。
可重复读是怎么实现的？
可重复读通过 数据快照（MVCC） 和 间隙锁 实现，
保证事务内多次查询结果一致，且防止其他事务插入新数据（解决幻读）。
读操作
数据快照（MVCC）
事务启动时：对数据库拍一张“快照”（记录当前已提交的数据版本）。
后续所有查询：都基于这个快照读取数据，无视其他事务的修改。
效果：事务内多次查询同一数据，结果永远一致。
sql复制代码
-- 事务A第一次查询（返回100）SELECT balance FROM account WHERE id = 1;-- 事务B修改并提交（balance改为200）UPDATE account SET balance = 200 WHERE id = 1;COMMIT;-- 事务A第二次查询（依然返回100）SELECT balance FROM account WHERE id = 1;
间隙锁（Gap Lock）解决幻读本质还是SELECT ... FOR UPDATE（这个才会触发间隙锁，普通的select根本就做不到触发这个间隙锁）
锁定“空白区域”：防止其他事务在查询范围内插入新数据。
解决幻读：比如事务A查询 WHERE age > 20 后，事务B插入 age = 25 会被阻塞。
-- 事务A锁定20~30之间的“间隙”SELECT * FROM users WHERE age BETWEEN 20 AND 30 FOR UPDATE;-- 事务B插入age=25的数据会被阻塞INSERT INTO users (age) VALUES (25);
写加锁
对UPDATE, DELETE, INSERT 和 SELECT ... FOR UPDATE 等写操作或加锁读操作，采用加锁的方式。
当一个事务需要修改某行数据时，它必须先获取该行的排他锁（写锁）。
如果获取成功，它将持有该锁直到事务结束。
如果该行已被其他事务锁定，当前事务的写操作就会阻塞等待。
这种**“先锁后改”的机制，将并发的写操作强制转换为了串行执行**，从而从根本上杜绝了多个事务基于同一个旧值进行计算，并最终导致更新被覆盖的问题
核心特点
读操作：基于快照，结果永远一致。
写操作：基于最新数据，并加锁防止冲突。
通过间隙锁彻底解决幻读（标准SQL的可重复读允许幻读）。
想象你在读一本正在更新的书：
快照：你开始读时复印了全书，之后只读复印件，无视新写的章节。
间隙锁：你预定要读的章节范围，禁止作者在范围内插入新内容。
四种标准隔离级别（由低到高）
隔离级别 脏读 不可重复读 幻读 实现机制 性能 典型应用场景 读未提交（Read Uncommitted） 允许 允许 允许 无锁（直接读最新数据） 最高 极少使用，仅临时数据分析 读已提交（Read Committed） 禁止 允许 允许 行级锁（写锁）、MVCC快照读 较高 默认级别（如Oracle） 可重复读（Repeatable Read） 禁止 禁止 允许* 行级锁 + 间隙锁（InnoDB）、MVCC 中等 MySQL默认级别（事务一致性要求高） 串行化（Serializable） 禁止 禁止 禁止 表级锁（读写均加锁） 最低 强一致场景（如金融交易）

