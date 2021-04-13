---
title: SQLite
date: 2021-03-29 11:36:14
tags:
---
### 文档指南：
https://www.sqlite.org/index.html


### 文章推荐：
https://antonz.org/sqlite-is-not-a-toy-database/?continueFlag=4468f03238b1209651088b2e0490953e


### 详细讲诉
- 在 Chrome、Safari 和 Firefox 等浏览器客户端中使用 WebSQL 时，会直接操作 SQLite。
(https://developer.chrome.com/docs/devtools/storage/websql/)

可以打开这个网址（https://andrew.hedges.name/html5/sql.html）—— 里面还有很多别的实验


实际上 SQLite 本身是一个嵌入式的开源数据库引擎，大小只有 3M 左右，可以将整个 SQLite 嵌入到应用中，而不用采用传统的客户端／服务器（Client/Server）的架构。这样做的好处就是非常轻便，在许多智能设备和应用中都可以使用 SQLite，比如微信就采用了 SQLite 作为本地聊天记录的存储。


SQLite 是在 2000 年发布的，到目前为止已经有 19 年了。一直采用 C 语言编写，采用 C 语言而非 C++ 面向对象的方式，可以提升代码底层的执行效率。

但 SQLite 也有一些优势与不足。它的优势在于非常轻量级，存储数据非常高效，查询和操作数据简单方便。此外 SQLite 不需要安装和配置，有很好的迁移性，能够嵌入到很多应用程序中，与托管在服务器上的 RDBMS 相比，约束少易操作，可以有效减少服务器的压力。

不足在于 SQLite 常用于小到中型的数据存储，不适用高并发的情况。比如在微信本地可以使用 SQLite，即使是几百 M 的数据文件，使用 SQLite 也可以很方便地查找数据和管理，但是微信本身的服务器就不能使用 SQLite 了，因为 SQLite 同一时间只允许一个写操作，吞吐量非常有限。

作为简化版的数据库，SQLite 没有用户管理功能，在语法上也有一些自己的“方言”。比如在 SQL 中的 SELECT 语句，SQLite 可以使用一个特殊的操作符来拼接两个列。在 MySQL 中会使用函数 concat，而在 SQLite、PostgreSQL、Oracle 和 Db2 中使用||号，比如：SELECT MesLocalID || Message FROM "Chat_1234"。

这个语句代表的是从 Chat_1234 数据表中查询 MesLocalID 和 Message 字段并且将他们拼接起来。

但是在 SQLite 中不支持 RIGHT JOIN，因此你需要将右外连接转换为左外连接，也就是 LEFT JOIN，写成下面这样：SELECT * FROM team LEFT JOIN player ON player.team_id = team.team_id

除此以外 SQLite 仅支持只读视图，也就是说，我们只能创建和读取视图，不能对它们的内容进行修改。


总的来说支持 SQL 标准的 RDBMS 语法都相似，只是不同的 DBMS 会有一些属于自己的“方言”，我们使用不同的 DBMS 的时候，需要注意。


我今天讲了有关 SQLite 的内容。在使用 SQLite 的时候，需要注意 SQLite 有自己的方言，比如在进行表连接查询的时候不支持 RIGHT JOIN，需要将其转换成 LEFT JOIN 等。同时，我们在使用 execute() 方法的时候，尽量采用带有参数的 SQL 语句，以免被 SQL 注入攻击。

### better-sqlite
文档指路：https://github.com/JoshuaWise/better-sqlite3/tree/4dc52f1dce355fc5894edf0566f8fd3eb0af214f

<pre>
The fastest and simplest library for SQLite3 in Node.js.
Node.js中最快、最简单的SQLite3库。

Full transaction support
完全的事务支持
High performance, efficiency, and safety
高性能、高效率和安全性
Easy-to-use synchronous API (better concurrency than an asynchronous API... yes, you read that correctly)
易于使用的同步API（比异步API有更好的并发性......是的，你没看错）
Support for user-defined functions, aggregates, and extensions
支持用户定义的函数、集合和扩展。
64-bit integers (invisible until you need them)
64位整数(在你需要之前是不可见的)
Worker thread support (for large/slow queries)
工作线程支持（用于大型/慢速查询）https://nodejs.org/api/worker_threads.html
</pre>

提供了benchmark(https://en.wikipedia.org/wiki/Benchmark_(computing))
<pre>
Benchmark
To run the benchmark yourself:

git clone https://github.com/JoshuaWise/better-sqlite3.git
cd better-sqlite3
npm install # if you're doing this as the root user, --unsafe-perm is required
node benchmark
</pre>


<pre>
When is this library not appropriate?
什么时候不适合使用这个库？

In most cases, if you're attempting something that cannot be reasonably accomplished with better-sqlite3, it probably cannot be reasonably accomplished with SQLite3 in general. For example, if you're executing queries that take one second to complete, and you expect to have many concurrent users executing those queries, no amount of asynchronicity will save you from SQLite3's serialized nature. Fortunately, SQLite3 is very very fast. With proper indexing, we've been able to achieve upward of 2000 queries per second with 5-way-joins in a 60 GB database, where each query was handling 5–50 kilobytes of real data.
在大多数情况下，如果你正在尝试一些不能用better-sqlite3合理完成的事情，那么一般情况下可能也不能用SQLite3合理完成。例如，如果你正在执行需要一秒钟才能完成的查询，并且你期望有许多并发用户执行这些查询，那么再多的异步性也无法将你从SQLite3的序列化特性中拯救出来。幸运的是，SQLite3的速度非常非常快。通过适当的索引，我们已经能够在一个60GB的数据库中用5路连接实现每秒高达2000次的查询，其中每个查询都要处理5-50kb的真实数据。

If you have a performance problem, the most likely causes are inefficient queries, improper indexing, or a lack of WAL mode—not better-sqlite3 itself. However, there are some cases where better-sqlite3 could be inappropriate:
如果你有性能问题，最有可能的原因是查询效率低下，索引不当，或者缺乏WAL模式，而不是better-sqlite3本身。然而，在某些情况下，better-sqlite3可能是不合适的。

If you expect a high volume of concurrent reads each returning many megabytes of data (i.e., videos)
如果你期望大量的并发读取，每个返回许多兆字节的数据（即视频）。
If you expect a high volume of concurrent writes (i.e., a social media site)
如果你期望有大量的并发写入（例如，一个社交媒体网站）。
If your database's size is near the terabyte range
如果您的数据库的大小接近TB的范围

For these situations, you should probably use a full-fledged RDBMS such as PostgreSQL.
对于这些情况，你可能应该使用一个成熟的RDBMS，如PostgreSQL。
</pre>

### 延伸阅读
- https://nodesource.com/blog/worker-threads-nodejs/
- https://blog.insiderattack.net/deep-dive-into-worker-threads-in-node-js-e75e10546b11


### 工具推荐
navicat
datagrip
- 数据库建模
PDMan (http://www.pdman.cn/#/)
PD(PowerDesigner)