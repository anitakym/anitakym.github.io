---
title: SQL学习笔记之基础介绍
date: 2020-12-22 16:48:30
tags:
    - sql
---

• DBS
	◦ DataBase System，数据库系统
	◦ 包括数据库、数据库管理系统以及数据库管理人员 DBA

• DBMS
	◦ DataBase Management System，数据库管理系统
	◦ 实际上它可以对多个数据库进行管理， DBMS = 多个数据库（DB） + 管理程序

• 排名
	◦ https://db-engines.com/en/
	◦ https://db-engines.com/en/ranking


• NoSQL泛指非关系型数据库——
	◦ 键值型数据库
		‣ key-value的方式来存储数据
		‣ key:唯一标识符
		‣ 查找速度快，但无法自由的使用条件过滤
		‣ 使用场景——作为内容缓存
		‣ 例如：redis
	◦ 文档型数据库
		‣ 文档作为处理信息的基本单位
		‣ 一个文档相当于一条记录
		‣ 例如：mongoDB
	◦ 搜索引擎
		‣ 全文索引，核心原理是“倒排索引”
		‣ 例如：Elasticsearch,Splunk,Solr
	◦ 列式数据库
		‣ 相对于行式（Row-based:Oracle，MySQL，SQL Server）
		‣ 大量降低系统IO
		‣ 适合分布式文件系统
		‣ 不足在于功能相对有限
	◦ 图形数据库
		‣ 用图存储实体之间的关系
		‣ 数据模型以节点和边（关系）来实现
		‣ 能高效的解决负责的关系问题


• Oracle
	◦ 第一个商用RDBMS
• MySQL
	◦ 1995
	◦ 开源数据库管理系统
	◦ 2008，被SUN收购，2010，SUN被Oracle收购
	◦ MariaDB
• SQL Server
	◦ 微软，1989
	◦ 微软还有Access（2G）—— 轻量级桌面数据库


> NoSQL最早是想远离SQL，随着发展，越来越离不开SQL; NoSQL是对SQL很好的补充
