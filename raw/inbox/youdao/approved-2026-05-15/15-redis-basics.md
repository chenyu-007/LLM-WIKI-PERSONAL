---
source: youdao-note
youdao_id: WEB300dbb9950539a75f3e2b20fcde99d14
title: Redis常识.note
captured: 2026-05-15
status: pending-review
---

Redis常识
Redis 与 MySQL 截然不同：它无表无结构，同一个 key 可随意变更类型（如从字符串变哈希），重启默认丢数据，不设过期则内存永不释放；6.0 前仅靠单一密码控制全局权限，极易被“删库跑路”；删除大 key 不立即回收内存，查询能力极弱，必须“写时设计读路径”，靠预计算和空间换时间实现高性能；但它的string支持二进制安全存储，可直接缓存图片、对象、压缩数据
Redis 没有表、没有列、没有数据类型约束，同一个 key 可以今天存字符串明天变列表！
MySQL：必须先 CREATE TABLE，定义字段、类型、索引、约束。
Redis：直接 SET key value，没有任何结构限制。
你可以对一个 key 先 SET，再 HSET，Redis 会直接覆盖并改变类型 —— 不报错！ 
Redis 是内存数据库，默认情况下服务器重启，所有数据消失！
MySQL：数据天然落盘，重启后数据还在。
Redis：默认无持久化配置（早期版本），或仅异步 RDB 快照 —— 宕机可能丢几分钟数据。
Redis 默认不自动清理数据！不设过期时间 = 永久占用内存！
MySQL：数据一直存在，但磁盘便宜，一般不担心“爆炸”。
Redis：内存昂贵，若忘记设 EXPIRE，数据会一直堆积
Redis 6.0 之前，只要知道密码，就能执行 FLUSHALL、SHUTDOWN！
MySQL：支持多用户、细粒度权限（库/表/列/操作）。
Redis（<6.0）：一个密码，全实例权限 —— 删库、关机、改配置，无所不能。
💡 曾有多少公司 Redis 被黑客通过弱密码攻入，执行 FLUSHALL 清库？
Redis删除一个大 Key，可能不会立即释放内存，而是“慢慢”回收！
MySQL：DELETE 后空间可被 InnoDB 重用或通过 OPTIMIZE 回收。
Redis：删除大 Key（如百万级 List/Hash）时，为避免阻塞主线程，采用“懒删除”或“异步删除”（取决于版本和配置）。
Redis 排序和查询能力极弱，只能按“key”或“预设结构”访问！
MySQL：SELECT * FROM users WHERE age > 18 ORDER BY name
Redis：你必须事先设计好数据结构，比如：
用 Sorted Set 存年龄 → ZRANGEBYSCORE users:age 18 +inf
用 Set 存标签 → SMEMBERS tag:python
无法实现“跨维度”、“动态条件”查询
💡 Redis 是“读写路径优化”，不是“查询优化”。它要求你“写入时就规划好怎么读”    “空间换时间” + “预计算”思想，避免运行时计算 —— 这是 Redis 高性能的核心哲学。
Redis String 可以存图片、序列化对象、甚至是压缩数据！
MySQL：VARCHAR 有字符集、长度限制，BLOB 类型才存二进制。
Redis：String 是“二进制安全”的字节数组 —— 你可以 SET key "$(cat image.jpg)"，完全没问题！
💡 很多人不知道 Redis 可以直接缓存图片、Protobuf、Gzip 内容等。
Redis 最常用的 5 种数据结构
 1. String（可以理解为变量，因为基础类型string int都能存）
存单个值：用户 Token、计数器、缓存 HTML/JSON、分布式锁
也能存图片、二进制数据（比如序列化后的对象）
常用命令：
# 设置值SET mykey "Hello Redis"# 获取值GET mykey→ "Hello Redis"# 设置并带过期时间（10秒后自动删除）SETEX mykey 10 "临时数据"# 数字自增（原子操作！多线程安全）SET counter 10INCR counter   # → 11INCRBY counter 5  # → 16# 批量设置/获取MSET name "Alice" age 25 city "Beijing"MGET name age city→ "Alice" "25" "Beijing"
底层实现：
Redis 不是用普通字符串，而是用 SDS（Simple Dynamic String）：

二进制安全 → 能存图片、压缩数据、带 \0 的内容
✅ 小贴士：如果你存的是数字，Redis 会优化成 int 编码，省内存！

避坑：
❌ 不要存超大字符串（> 10MB），会阻塞 Redis
✅ 一定要设过期时间！否则数据永远在内存里！
2. Hash（哈希）
字典里的字典，一个key但是多个value 
存一个对象的多个字段：用户资料（name, age, email）、商品信息
比用多个 String key 更省内存、更易管理
常用命令：
# 设置对象字段HSET user:1001 name "Alice" age 25 email "alice@example.com"# 获取单个字段HGET user:1001 name→ "Alice"# 获取所有字段和值HGETALL user:1001→ name Alice age 25 email alice@example.com# 获取多个字段HMGET user:1001 name age→ "Alice" "25"# 删除字段HDEL user:1001 email# 自增数字字段（原子操作）HINCRBY user:1001 age 1  # → 26
底层实现：
数据少时用 ziplist（压缩列表） → 内存连续，非常紧凑（省内存）
 ziplist  把 field 和 value 连续紧凑地存在一块内存里，没有指针、没有额外结构，极致省内存！ziplist 是一块连续的内存区域，每个 field 和 value 挨着存储，像数组一样但查找时要从头到尾遍历 → O(N) 时间复杂度
数据多时自动转成 hashtable（哈希表） → 查询快 O(1)
内部用“哈希索引” —— 给每个项目名算一个“编号”，直接跳到对应位置小贴士：默认字段数 ≤ 512 且每个值 ≤ 64 字节时用 ziplist —— 自动优化！
 ziplist（压缩列表） hashtable（哈希表） 内存占用 ⭐⭐⭐⭐⭐ 极小（连续存储） ⭐⭐ 较大（指针+结构体） 查询速度 ⭐⭐ O(N) 遍历（数据少时快） ⭐⭐⭐⭐⭐ O(1) 直接定位

避坑：
❌ 不要用 HGETALL 取超大 Hash（比如存了 10 万个字段）→ 会卡住 Redis
✅ 用 HSCAN 分批获取大数据量
3. List（列表）
队列”或“栈”：
最新消息列表（朋友圈、评论）
任务队列（生产者放，消费者取）
栈结构（LIFO）、队列结构（FIFO）
常用命令：
# 从左边插入（像“压栈”或“队列头部插入”）LPUSH mylist "first" "second"# 从右边插入（像“入队尾”）RPUSH mylist "third"# 查看所有元素（0 到 -1 表示全部）LRANGE mylist 0 -1→ "second" "first" "third"# 从左边弹出（消费队列）LPOP mylist→ "second"# 从右边弹出（像“出栈”）RPOP mylist→ "third"# 阻塞弹出（没数据时等10秒，用于消费者）BLPOP mylist 10
底层实现：
Redis 3.2+ 用 quicklist = “双向链表 + 每个节点是 ziplist”

既避免链表内存碎片
又避免 ziplist 太大导致修改慢
✅ 小贴士：插入/删除头尾元素极快（O(1)），中间操作慢（O(N)）→ 所以适合做队列！

避坑：
❌ 不要用 LRANGE key 0 -1 取超大 List（比如100万条）→ 会卡死
✅ 用 LRANGE key 0 9 分页取前10条
❌ 不要用 List 存“需要随机访问中间元素”的数据
4. Set（集合）
自动去重，支持交并差
用途：
标签系统（一篇文章有哪些标签）
共同好友（A 和 B 的好友交集）
抽奖（SPOP 随机弹出不重复）
去重统计（今天有哪些用户访问过）
🚀 常用命令：
# 添加元素（自动去重）SADD tags:post1 "redis" "database" "nosql" "redis"  # 最后一个 redis 被忽略# 查看所有元素SMEMBERS tags:post1→ "database" "redis" "nosql"# 判断元素是否存在SISMEMBER tags:post1 "redis"→ 1（存在）或 0（不存在）# 随机弹出一个（抽奖用）SPOP tags:post1→ "nosql"# 求两个集合的交集（共同标签）SADD tags:post2 "redis" "cache" "system"SINTER tags:post1 tags:post2→ "redis"# 求并集、差集SUNION set1 set2SDIFF set1 set2  # set1 有但 set2 没有的
底层实现：
元素全是整数 + 数量少 → 用 intset（整数集合） → 内存紧凑，有序，支持二分查找
含字符串或数量多 → 用 hashtable → O(1) 查找，值为 NULL
✅ 小贴士：Set 的“成员”必须唯一，重复添加无效 —— 天然防重！

避坑：
❌ 不要用 SMEMBERS 取超大 Set（比如百万级）→ 用 SSCAN 分批
✅ Set 不保证顺序（和 List 不同）→ 不要用它存“有序列表”
5. Sorted Set ：ZSet /有序集合 
带分数的 Set，自动排序！
排行榜（游戏积分、带货销量）
延迟队列（用时间戳当分数）
范围查找（分数 80~100 的学生）
🚀 常用命令：
# 添加成员 + 分数ZADD leaderboard 100 "Alice" 200 "Bob" 150 "Charlie"# 按排名取（0 是第1名，-1 是最后一名）ZRANGE leaderboard 0 -1 WITHSCORES→ "Alice" "100" "Charlie" "150" "Bob" "200"# 按分数范围取（80 到 200 分）ZRANGEBYSCORE leaderboard 80 200 WITHSCORES# 获取某人的排名（从低到高）ZRANK leaderboard "Alice"→ 0（第1名）# 获取某人的分数ZSCORE leaderboard "Bob"→ "200"# 给某人加分ZINCRBY leaderboard 10 "Alice"  # → 110# 删除某人ZREM leaderboard "Charlie"
底层实现：
同时用 skiplist（跳跃表） + hashtable
hashtable → 通过成员名 O(1) 找分数
skiplist → 按分数排序，支持范围查询 O(log N)
✅ 小贴士：跳跃表 = 多层链表，比平衡树好实现，适合并发 —— 所以 Redis 选它！
新手避坑：
❌ 分数（score）是 double 类型，注意精度问题
✅ 成员（member）必须唯一，重复添加会更新分数
❌ 不要频繁对大量元素做 ZRANGE，用 ZREVRANGE + LIMIT 分页
一句话总结选型：
你想做什么？ 用哪个结构？ 一句话口诀 存一个值（Token/计数器） String “单值缓存用 String” 存一个对象（用户资料） Hash “对象字段用 Hash” 做队列/最新列表 List “队列栈结构用 List” 去重/标签/共同好友 Set “去重集合用 Set” 排行榜/按分数排序 Sorted Set “带分排序用 ZSet”
🧭 建议：
先从 String 和 Hash 开始 —— 最常用，最容易理解
每个命令都在 redis-cli 里亲手敲一遍 —— 比看10遍文档都管用
数据一定要设过期时间 —— 避免内存爆炸
大 key（List/Set/ZSet 超几千元素）不要用 ALL 命令 —— 用 SCAN/LRANGE 分页
用 TYPE key 和 OBJECT ENCODING key 查看类型和底层编码 —— 加深理解
LRANGE 分页
 —— 用于 List（列表）
什么是 LRANGE？
LRANGE key start stop —— 取 List 中从 start 到 stop 的元素（包含两端）
0 表示第一个元素
-1 表示最后一个元素
10 表示第 11 个（从 0 开始计数）
分页怎么用？
假设你的 List 有 1000 个元素，你想分批取，每页 10 条：
# 第1页：取第 0 ~ 9 条LRANGE mylist 0 9# 第2页：取第 10 ~ 19 条LRANGE mylist 10 19# 第3页：取第 20 ~ 29 条LRANGE mylist 20 29# ... 以此类推
你不会让 App 一次性加载 1000 个视频 → 卡死手机
而是“刷10个 → 再刷10个 → 再刷10个”
实用技巧：
用 LLEN key 先获取总长度，计算总页数
前端/客户端循环调用，每次 start = (page-1)*size, stop = page*size - 1
LLEN mylist→ 1000# 每页10条，共100页# 第5页：start=40, stop=49LRANGE mylist 40 49
SCAN 分页 
 用于 Set / Hash / ZSet / 全库 Key
为什么 List 用 LRANGE，而 Set 不能用 “SRANGE”？
因为：
List 是有序的 → 你知道第 0 个、第 1 个是谁
Set 是无序的 → 没有“第几个”的概念！
所以 Redis 提供了通用的 SCAN 系列命令：
数据结构 SCAN 命令 作用 数据库 Key SCAN cursor 扫描所有 key Hash HSCAN key cursor 扫描 Hash 的 field-value Set SSCAN key cursor 扫描 Set 的成员 ZSet ZSCAN key cursor 扫描 ZSet 的 member-score
SCAN 怎么用？（以 SSCAN 为例）
SSCAN = Set SCAN → 专门用来扫描 Set 类型的命令
myset = 你要扫描的 Set 的 key 名字
0 = cursor（游标），第一次扫描必须从 0 开始
COUNT 10 = “建议”这次返回大约 10 个元素（不是绝对精确！）
# 初始化：cursor = 0SSCAN myset 0 COUNT 10→ 1) "17"          # 下次用的 cursor（不是 0 表示没扫完）   2) 1) "member1"      2) "member2"      ... 共10个# 第二次：用返回的 cursorSSCAN myset 17 COUNT 10→ 1) "45"   2) 1) "member11"      2) "member12"      ...# 直到 cursor = 0，表示扫完了SSCAN myset 45 COUNT 10→ 1) "0"           # 扫描结束！   2) ... 最后一批元素
就像超市盘点库存 🛒：
店长不会说：“把所有商品一次性搬出来数！” → 累死，超市停业
而是：“今天数 A区货架，明天数 B区，后天数 C区...”
cursor 就是“盘点到哪个区了”的标记
关键参数：COUNT
COUNT 10：建议每次返回约 10 个元素（不是精确值！）
Redis 会尽量满足，但可能多可能少（尤其是 ziplist 编码时）
适合值：10~1000，根据网络和内存调整
LRANGE vs SCAN 核心区别
特性 LRANGE（List） SCAN（Set/Hash/ZSet） 是否有序 ✅ 有序，可按位置取 ❌ 无序，只能“游标式”遍历 是否精确分页 ✅ 精确（0~9 就是前10个） ❌ 不精确（COUNT 是“建议值”） 是否阻塞 ❌ 取大量数据会阻塞 ✅ 非阻塞（每次只取一小批） 适用场景 朋友圈、消息列表（有序+分页） 标签、用户列表（无序+遍历）

