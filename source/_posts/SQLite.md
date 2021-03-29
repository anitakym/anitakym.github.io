---
title: SQLite
date: 2021-03-29 11:36:14
tags:
---
文档指南：
https://www.sqlite.org/index.html


文章推荐：
https://antonz.org/sqlite-is-not-a-toy-database/?continueFlag=4468f03238b1209651088b2e0490953e


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


