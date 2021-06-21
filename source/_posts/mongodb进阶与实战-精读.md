---
title: mongodb进阶与实战-精读
date: 2021-05-25 14:11:28
tags:
---
## 入门

### 系统-分层来描述现实中的模型
  - 物理层-存储介质 ｜ 操作系统/FS-文件系统EXT4/XFS ｜ 数据库-数据表/行/文档 ｜ 应用程序-类/对象
  - 自下而上，上层用更简单易表述的模型来隐藏下层的复杂性
  - 数据库系统屏蔽来磁盘文件的存取压缩细节，给应用程序展示了一些通用的数据模型
  - 处理SQL数据模型 - ORM框架（hibernate等）
  - 基于JSON的文档模型更契合面向对象的设计准则

### BSON（一种二进制版本的JSON扩展）
  - 易用性扩展（增加日期，二进制的支持）

### 动态模式
  - 所有读写都是基于一种内部隐含的模式，模式采取按需变更而非提前声明

### Feature
#### 完备的索引
- 设计思路和一般关系型数据库差不多
- 特殊应用场景支持：地理空间，文本检索，TTL
#### 跨平台
- C++ write
- 3.4之后不再支持32-bit X86
- 提供了多种语言实现的驱动-Java/C/C++/C#/Python/NodeJS

#### aggregation很强大
- 以文档化模型为基础设计，适合非结构化数据
- pipline/stage

#### replication set 副本集
- 类似MySQL的Master/Slave复制架构
- 海量数据处理-原生支持分布式计算能力

### Advantage
#### 易用
- 变更文档结构无需执行DDL变更语句，方便业务平滑升级

#### 高性能
- 3.0-WiredTiger存储引擎（基于内存的二级缓存提供了高速读取数据的能力，根据磁盘I/O特点做了缓冲式写入）

#### 高可靠
- 单个MongoDB节点-开启Journal机制实现断电保护
- 集群节点-副本集架构（节点宕机，秒级切换）

#### 高可扩展
- 分片的集群架构

#### 社区支持

### Difficult
- 关系型数据库思维转变，关注段放在系统未来的扩展能力，专注做好表设计，访问模式和性能的权衡
- 事务-4.0之后支持（一致性要求高-金融交易类）

### 类比SQL模型
#### 类比
database（数据库）- 逻辑上名称的空间
collection （集合） - SQL中的表
document（文档）- 相当于数据表中的一行
field（字段）- 文档中的一个属性，相当于column（列）
index（索引）- 独立的检索式数据结构
_id - 相当于SQL中的primary key
view（视图） - 看作虚拟的集合，3.4版本中开始提供，通过聚合管道技术实现
$lookup（聚合操作）- 类似table join表链接的聚合操作符

#### 差异
- 半结构化（用的字段无需声明，支持多级嵌套，数组等灵活的数据类型）+弱关系（没有外键约束，也没有强大的表连接能力）

#### 类SQL语句
- ANSQL

## 安装
#### 包含的二进制程序
- mongod-数据库服务启动程序
- mongo-数据库客户端shell程序
- mongostat-数据库性能监控工具
- mongotop-热点表监控工具
- mongodump-数据库逻辑备份工具
- mongorestore-数据库逻辑恢复工具
- mongoexport-数据库导出工具
- mongoimport-数据库导入工具
- bsondump-BSON格式转换工具
- mongofiles-GridFS文件工具

### mongo shell
- mongodb是用来SpiderMonkey作为内部JavaScript引擎,3.2之前用的V8
- --eval 非交互式


## 操作
可见另外一篇博文 - mongodb


### 卸载
```
service mongod stop
yum erase $(rpm -qa | grep mongodb-org)
rm -rf /var/log/mongodb
rm -rf /var/lib/mongo
```