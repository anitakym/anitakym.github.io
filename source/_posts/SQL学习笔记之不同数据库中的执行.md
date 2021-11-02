---
title: SQL学习笔记之不同数据库中的执行
date: 2021-01-07 13:57:00
tags:
    - SQL
---
### Oracle中SQL的执行

#### SQL语句
	- 语法检查
		- 检查SQL拼写
	- 语义检查
		- 检查SQL中国内地访问对象是否存在
	- 权限检查
		- 看用户是否具备访问该数据的权限
	- 共享池检查
		- shared pool 内存池
			- 库缓存
				- 决定SQL语句是否需要进行硬解析
				- 如何避免硬解析——绑定变量：在SQL语句中使用变量，通过不同变量取值来改变SQL的执行结果
			- 数据字典缓冲区
				- 对象定义
				- 表，视图，索引等对象
				- 对SQL语句进行解析对适合，如果需要相关数据，会从数据字典缓冲区中提取
			- 缓存SQL语句和该语句的执行计划
		- Oracle通过检查是否存在SQL语句的执行计划，来判断进行软解析还是硬解析
		- 执行（软解析）
	- 优化器（硬解析）
		- 决定怎么做，比如创建解析树，生成执行计划
		- 执行
	- 执行器
		- 基于解析树+执行计划
		- 在执行器中执行语句


#### 如何避免硬解析，使用软解析？
oracle 绑定变量
```
select * from a where a_id = 10001
select * from a where a_id = :a_id
```
但是动态SQL因为参数不同，SQL的执行效率也不同，给SQL优化带来了困难

### MySQL
C/S架构
• 连接层
• SQL层
• 存储引擎层
### create database VS create schema
- mysql
    - CREATE DATABASE creates a database with the given name. To use this statement, you need the CREATE privilege for the database. 
    - CREATE SCHEMA is a synonym for CREATE DATABASE.
    -  https://dev.mysql.com/doc/refman/8.0/en/create-database.html

- SQL Server