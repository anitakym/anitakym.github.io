---
title: SQL学习笔记之基础介绍
date: 2020-12-22 16:48:30
tags:
    - sql
---


> 1946_ENIAC_Electronic Numerical Integrator And Computer_第一台通用电子计算机

### 引入

- I/O 是DBMS最容易出现瓶颈的地方
	- 数据库操作中大量时间花在了I/O 上面
  - 参考文档：https://docs.oracle.com/cd/B28359_01/server.111/b28274/iodesign.htm#PFGRF015
- 降低CPU的计算量
	- 在SQL语句中使用GROUP BY ，ORDER BY 等语句会消耗大量CPU计算资源
  - 参考文档：https://use-the-index-luke.com/sql/sorting-grouping
- 内存使用情况


- EXISTS  / IN  查询

```
SELECT * FROM A WHERE cc IN (SELECT cc FROM B)
SELECT * FROM A WHERE EXISTS IN (SELECT cc FROM B WHERE B.cc=A.cc)
```

- 有索引
	- 表A比表B大，IN子查询的效率比EXISTS子查询效率高


比如最大生命值大于 7000 的法师英雄都有谁，那么你会怎么做呢？
```
SELECT * FROM heros WHERE hp_max >= 7000 AND role = '法师'
```


 7 天内的新增用户数有多少，该怎么做呢？

```
SELECT COUNT(*) as num FROM new_user WHERE TO_DAYS(NOW())-TO_DAYS(regist_time)<=7
```

- 基于数据的各种技术中也会用到 SQL
	- OLTP（联机事务处理过程）
	- OLAP（联机分析处理过程）
	- RDBMS（对象关系型数据库管理系统）
	- 在 NoSQL 的阵营上，如今也在使用类似 SQL 的操作，要知道，提出 NoSQL 这个概念的初衷就是远离 SQL，但如今人们更愿意把 NoSQL 定义为 Not Only SQL（不只是 SQL）
	- 在 XML、JSON 等数据格式中，都存在着各种 SQL，比如用于 XML 的 SQL、用于 JSON 的 SQL 等
	- 用于记录地理位置信息的 SQL、用于搜索的 SQL、用于时间序列数据的 SQL、用于流的 SQL 等


### SQL
- TIPS
	- TIOBE(https://www.tiobe.com/tiobe-index/)


- 历史
	- https://zh.wikipedia.org/wiki/SQL
	- 在1970年代初，由IBM公司San Jose,California研究实验室的埃德加·科德发表将资料组成表格的应用原则（Codd's Relational Algebra）。
	- 1974年，同一实验室的D.D.Chamberlin和R.F. Boyce对Codd's Relational Algebra在研制关系数据库管理系统System R中，研制出一套规范语言-SEQUEL（Structured English Query Language），并在1976年11月的IBM Journal of R&D上公布新版本的SQL（叫SEQUEL/2）。
	- 1980年改名为SQL。
	- 目前，所有主要的关系数据库管理系统支持某些形式的SQL，大部分数据库至少遵守ANSI SQL89标准。
	- ANSI SQL92标准在交叉连接（cross join）和内部连接之上，新增加了外部连接，并支持在FROM子句中写连接表达式。支持集合的并运算、交运算。支持Case (SQL)表达式。支持CHECK约束。创建临时表。支持cursor。支持事务隔离。
	- SQL99


- 按功能划分
	- DDL
		- Data Definition Language
		- 定义数据库对象
			- 数据库
			- 数据表和列
		- 我们可以创建，修改和删除数据库和表的结构
	- DML
		- Data Manipulation Language
		- 操作和数据库相关的记录
			- 增，删，改数据表中的记录
	- DCL
		- Data Control Language
		- 定义访问权限和安全级别
	- DQL
		- Data Query Language


- 声明性语言
	- 不需要制定具体的执行步骤
- SQL语言定义了我们的需求
- 不同的DBMS会按照指定的SQL帮我们提取想要的结果

- RDBMS
	- 实体关系模型（Entity-Relationship Model），简称E-R Model，是陈品山（Peter P.S Chen）博士于1976年提出的一套数据库的设计工具，他运用真实世界中事物与关系的观念，来解释数据库中的抽象的资料架构。实体关系模型利用图形的方式（实体-关系图（Entity-Relationship Diagram））来表示数据库的概念设计，有助于设计过程中的构思及沟通讨论。

	- 设计—— ER图（Entity Relationship Diagram）实体——关系图
		- 用来描述现实世界的概念模型
		- 要素：实体——要管理的对象，属性——标识每个实体的属性，关系——对象之间的关系

	- ER图评审通过，用SQL语句或者可视化管理工具创建数据表-

- SQL大小写
	- 表名，表别名，字段名，字段别名——小写
	- SQL保留字，函数名，绑定变量——大写
- 数据表的字段名——下划线命名


### 数据库管理系统
- DBS
  - DataBase System，数据库系统
	- 包括数据库、数据库管理系统以及数据库管理人员 DBA

- DBMS
	- DataBase Management System，数据库管理系统
	- 实际上它可以对多个数据库进行管理， DBMS = 多个数据库（DB） + 管理程序

- 排名
	- https://db-engines.com/en/
  - https://db-engines.com/en/ranking


- NoSQL泛指非关系型数据库——
	- 键值型数据库
		- key-value的方式来存储数据
		- key:唯一标识符
		- 查找速度快，但无法自由的使用条件过滤
		- 使用场景——作为内容缓存
		- 例如：redis
	- 文档型数据库
		- 文档作为处理信息的基本单位
		- 一个文档相当于一条记录
		- 例如：mongoDB
	- 搜索引擎
		- 全文索引，核心原理是“倒排索引”
		- 例如：Elasticsearch,Splunk,Solr
	- 列式数据库
		- 相对于行式（Row-based:Oracle，MySQL，SQL Server）
		- 大量降低系统IO
		- 适合分布式文件系统
		- 不足在于功能相对有限
	- 图形数据库
		- 用图存储实体之间的关系
		- 数据模型以节点和边（关系）来实现
		- 能高效的解决负责的关系问题


- Oracle
	- 第一个商用RDBMS
- MySQL
	- 1995
	- 开源数据库管理系统
	- 2008，被SUN收购，2010，SUN被Oracle收购
	- MariaDB
- SQL Server
	- 微软，1989
	- 微软还有Access（2G）—— 轻量级桌面数据库


> NoSQL最早是想远离SQL，随着发展，越来越离不开SQL; NoSQL是对SQL很好的补充



### 参考学习项目
- mybatis-3
  - MyBatis SQL mapper framework for Java —— mybatis.github.io/mybatis-3/
	- 数据持久化