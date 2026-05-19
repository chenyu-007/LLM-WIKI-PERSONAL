---
source: youdao-note
youdao_id: WEB256b57ef0ea9fe4bd18f58f131646116
title: SQL调优专项.note
captured: 2026-05-15
status: pending-review
---

EXPLAIN 是什么？
主要是看sql语句查询到底用没用索引，扫了多少行？
假设你有一条查询：
SELECT * FROM users WHERE age = 25;
在前面加上 EXPLAIN：
EXPLAIN SELECT * FROM users WHERE age = 25;
它不会执行这条 SQL，而是返回一张表，告诉你执行这条 SQL 时会怎么干：
id select_type table type possible_keys key rows Extra 1 SIMPLE users ALL NULL NULL 1000 Using where
这表格的字段含义如下：
✅ 常看字段解释：
字段名 含义 type 访问类型，越靠后效率越低，ALL是全表扫描，ref/const是用索引 rows 预计要读取的行数。越少越好。 key 实际使用了哪个索引。NULL 表示没用索引。 Extra 附加信息，比如是否使用了临时表、排序、是否是 Using where 等。
索引优化例子
-- 没有索引的情况EXPLAIN SELECT * FROM users WHERE age = 25;
返回：
type: ALLrows: 100000key: NULL
表示它要全表扫描所有行找 age = 25。
-- 建立索引CREATE INDEX idx_age ON users(age);
再查：
EXPLAIN SELECT * FROM users WHERE age = 25;
现在返回：
type: refrows: 20key: idx_age
说明数据库现在只需要扫 20 行，性能立刻提升！
EXPLAIN看哪些参数？
type 是 ALL？
说明它在全表扫，可能没走索引。
rows 很大？
表示查了很多行，应该考虑索引。
Extra 有 "Using filesort"？
表示用了外部排序，可能要加排序字段索引。外部排序（External Sort）是数据库在内存不足以完成排序任务时，将部分数据写入磁盘临时文件、分段排序、再归并的过程；数据库就需要把所有行取出、按 created_at 排序。如果数据量超过了 sort_buffer_size（每个线程的排序内存），就会使用磁盘临时文件进行排序，也就是外部排序。为什么外部排序性能差？磁盘 IO 成本远高于内存；外部排序过程复杂（分段、写盘、读盘、归并）；容易让排序成为慢 SQL 的主要瓶颈。
Extra 有 "Using temporary"？
表示用了临时表，可能是 group by + order by 没加索引。
容易踩坑的 SQL 性能问题?
1. 全表扫描（Missing Index）
坑例：
SELECT * FROM users WHERE email = 'alice@example.com';
如果 users.email 没有建立索引，这条 SQL 会对整张表逐行扫描（全表扫），即使你只有一个用户叫 Alice。
改进：
-- 确保有索引CREATE INDEX idx_email ON users(email);-- 然后再执行查询SELECT * FROM users WHERE email = 'alice@example.com';
数据库索引底层一般是 B+ 树（或变种）：
插入/删除/查找的平均复杂度是 O(log N)；
而全表扫描是 O(N)，尤其对大表性能差异巨大。
索引本质：
是数据库维护的一个额外的数据结构，它保存了某些字段的有序副本 + 指向原始行的指针
🔍 explain 看区别：
未建索引时 type: ALL，表示全表扫描；建了索引后是 type: ref 或 const，效率高很多。
EXPLAIN 是 SQL 语句前加的一个关键字，用于 分析查询执行计划，帮助你理解数据库在执行这条 SQL 时会怎么查表、用不用索引、读几行数据、怎么关联表等。
它是 SQL 优化的最重要工具之一。
 2. 什么是 N+1 查询？
这是很多初学者和 ORM 用户经常踩的坑：
你本来想查 1 次数据库，结果查了 N+1 次！
你有两张表：
posts(id, title)         -- 文章表  comments(id, post_id, content)  -- 评论表（每篇文章有多条评论）
你想获取 所有文章及其对应的评论：
❌ 你可能写了这样的代码（伪代码）：
posts := db.Query("SELECT * FROM posts")  // 1 次查询for post in posts {    comments := db.Query("SELECT * FROM comments WHERE post_id = ?", post.id)  // N 次查询}
结果：1 + N 次查询（比如有 100 篇文章 → 查询了 101 次！）因为数据库连接、查询、网络传输是有代价的，一般跨网络或磁盘 IO，N 次比 1 次慢很多倍。
🌟 改写为 SQL JOIN：
SELECT posts.*, comments.*FROM postsLEFT JOIN comments ON posts.id = comments.post_id;
3. IN 子句或子查询过大
WHERE xxx IN (...) 是我们写 SQL 时很常见的语法，但一旦 IN 的值非常多，或者 IN 里是个子查询，就很容易出现性能问题。
你有张大表 orders（订单表），想找出「所有某些用户的订单」。
 写法一（长 IN 列表）：
SELECT * FROM ordersWHERE user_id IN (1001, 1002, 1003, ..., 9999);  -- 几千上万个 ID
如果这个 IN 列表长达几千个值，MySQL 在优化器层面很难进行高效优化，执行计划中会进行大量 OR 条件判断或临时表构建，导致查询变慢甚至崩溃。
写法二（子查询 IN）：
SELECT * FROM ordersWHERE user_id IN (  SELECT id FROM users WHERE last_login < '2024-01-01');
这个写法看起来没毛病，但 MySQL 对子查询的执行方式依赖执行器实现，老版本甚至会先执行外层，再逐条查子查询结果（效率极差）。
方法一：改为 JOIN（推荐）
SELECT o.*FROM orders oJOIN users u ON o.user_id = u.idWHERE u.last_login < '2024-01-01';
优化器可以利用索引优化 JOIN；
执行逻辑清晰可控，且 JOIN 更易被索引加速。
方法二：提前将 IN 的内容查出到程序里，批量分页执行
// 拿到用户 ID 列表userIDs := db.Query("SELECT id FROM users WHERE last_login < '2024-01-01'")// 每次分批处理100个IDfor batch in split(userIDs, 100) {    orders := db.Query("SELECT * FROM orders WHERE user_id IN (?)", batch)}
适用于你要处理上万个 ID，不适合直接拼接一个超长 IN 的场景；
能避免单条 SQL 太复杂。
如何定位到慢SQL？
1. 来自业务和用户的反馈（被动发现）
最直接的信号: “这个页面加载好慢！”、“这个查询按钮点了半天没反应！”
缺点: 这是最糟糕的情况。当用户都开始抱怨时，说明问题已经很严重了，而且你非常被动。
2. 应用性能监控 (APM) 系统（主动发现）
这是现代开发中最主流、最高效的方式。APM系统（如 SkyWalking, Pinpoint, New Relic, Datadog）能帮你：
自动发现慢接口: APM会列出响应时间最长的API接口列表。
追踪调用链: 你可以点开一个慢接口，看到它内部所有操作的耗时，包括对数据库的SQL查询。
定位慢SQL: APM会直接告诉你，是哪条SQL语句执行了多少次，平均耗时和总耗时是多少。这能让你精确地定位到问题SQL。
3. 数据库自身的慢查询日志 (DBA常用)
慢查询日志 = 数据库自己记录下来的“哪些 SQL 跑得特别慢”，以便你发现和优化它们。
几乎所有的数据库（MySQL, PostgreSQL等）都提供了慢查询日志功能。
如何开启 (以MySQL为例):
在数据库配置文件（my.cnf）中设置：
slow_query_log = 1  # 开启慢查询日志slow_query_log_file = /var/log/mysql/mysql-slow.log # 日志文件路径long_query_time = 1 # 定义超过多少秒的查询被认为是“慢查询”（比如1秒）log_queries_not_using_indexes = 1 # 记录没有使用索引的查询（非常有用！）
如何进行SQL调优
当你定位到一条慢SQL后，调优就正式开始了。核心工具是 EXPLAIN (或 EXPLAIN ANALYZE)。
EXPLAIN SELECT * FROM users WHERE name = 'alice';
这条命令会告诉你，数据库打算如何执行你的SQL查询。它不会真的执行查询，而是返回一个“执行计划”。你需要重点关注以下几个列：
type: 连接类型。性能从好到坏：system > const > eq_ref > ref > range > index > ALL。
如果看到 ALL，意味着全表扫描，这是性能杀手，通常是优化的首要目标。
possible_keys: 可能会用到的索引。
key: 实际用到的索引。如果是NULL，说明没有使用任何索引。
rows: 估算的需要扫描的行数。这个数字越小越好。
Extra: 额外信息，非常重要。
Using filesort: 意味着需要在磁盘或内存中进行额外的排序操作，性能很差。通常是因为ORDER BY的字段没有索引。
Using temporary: 意味着创建了临时表来处理查询，性能极差。通常是因为GROUP BY或UNION操作复杂。
Using index: 好事！表示查询所需的数据，只用在索引树里就能找到，都不用回表查数据行。这叫“覆盖索引”。
具体的调优方法：
加索引 (Indexing):
这是最最最常用、效果最显著的调优手段，能解决80%以上的问题。
原则:
1.在WHERE子句中经常用于查询条件的列上加索引。
2.在JOIN操作的连接列（ON后面的列）上加索引。（因为 JOIN 需要根据连接列匹配两张表的行，没有索引就只能暴力比对。）
3.在ORDER BY和GROUP BY的列上加索引，以避免Using filesort和Using temporary。
因为排序和分组时，如果没有索引，数据库就要使用临时表 + 文件排序（Using filesort），代价非常大，尤其是数据量一多。
SELECT * FROM logs ORDER BY created_at DESC LIMIT 100;
created_at 没有索引：数据库读完所有行再进行排序。
有索引：数据库直接按索引顺序读取前 100 行，无需排序。
以 B+ 树为例（MySQL 的 InnoDB 索引就是 B+ 树）：
索引按顺序存储 create_time；
LIMIT 100 只需要从最小节点开始往下遍历 100 次；
不需要排序，也不需要扫描全表。因此这个优化非常强大。
 explain 会显示是否用了 Using filesort 或 Using temporary，是性能警告信号。
4.创建联合索引: 如果你经常同时用多个列查询（如WHERE a = ? AND b = ?），创建一个(a, b)的联合索引通常比两个单独的索引效果更好。注意最左前缀原则。
改写SQL语句 (SQL Rewriting):
避免SELECT *: 只查询你真正需要的列。如果查询的列都能被一个索引覆盖（覆盖索引），性能会极大提升。
避免在WHERE子句中对字段进行函数操作或计算: WHERE YEAR(create_time) = 2025 无法使用create_time的索引。应改为 WHERE create_time >= '2025-01-01' AND create_time < '2026-01-01'。
使用UNION ALL代替UNION: 如果你确定结果集没有重复，用UNION ALL可以避免一次去重排序，性能更好。
小表驱动大表: 在多表JOIN时，尽量让结果集小的表作为驱动表。INNER JOIN时优化器会自动选择，但LEFT JOIN时左边的表是驱动表，需要注意。
选择合适的数据类型（比如用INT存IP地址而不是VARCHAR）。

