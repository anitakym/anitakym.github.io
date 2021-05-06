---
title: mongodb
date: 2021-04-23 22:15:30
tags:
---
> 精读-学习笔记
## Basic

### docs
- https://docs.mongodb.com/guides/
- https://university.mongodb.com/?tck=docs_landing
- 中文社区-https://mongoing.com/

### intro
- DB-Engines 排名
- 重新定义OLTP数据库 - （tips:OLAP）
- JSON Document 以JSON为数据模型的文档数据库
- MongoDB Inc.
- 建模可选/横向扩展可以支撑很大的数据量和并发
- 社区版（SSPL）/企业版（商业协议）
- 数据容量-理论上没有上限

### history
0.x 2008
1.x 2010 - 支持复制集（高可用）和分片集
2.x 2012 - 数据库功能
3.x 2014 - WiredTiger + 生态
4.x 2018 - 分布式事务支持

### advantage
- 面向开发者的易用&&高效数据库
- 对象模型（Objects=>Database）—— 传统关系数据库，复杂的关系模型
- 快速响应业务变化（可动态增加新字段）
  - 多形性:同一个集合中，可以包含不同字段的文档对象
  - 动态性：线上修改数据模式，修改时应用与数据库均无需下线
  - 数据治理：支持使用JSON Schema来规范数据模式。在保证模式灵活动态的前提下，提供数据治理能力
- JSON模型（快速灵活）
  - 数据库引擎只需要在一个存储区读写（对物理存储有优势，节约了定位时间）
  - 反范式，无关联的组织极大优化查询速度
  - 程序API自然，开发快速（API查询）
- 分布式（原生的高可用）
  - Replica Set 复制集（2-50个成员）3个节点以上
  - 自动恢复
  - 多中心容灾
  - 滚动服务-最小化服务终端（无需下线）
- 横向扩展能力
  - 需要的时候无缝扩展
  - 对应用全透明
  - 多种数据分布策略
  - 支持TB-PB数量级
  
### install
- 企业/社区
- 偶数版
- version/os/package
- https://docs.mongodb.com/manual/administration/install-community/
```
# linux - 自己下载安装
mkdir -p /data /data/db
cd /data
curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-4.2.1.tgz
tar -xvf mongodb-linux-x86_64-rhel70-4.2.1.tgz
export PATH=$PATH:/data/mongodb-linux-x86_64-rhel70-4.2.1/bin
mongod --dbpath /data/db --port 27017 --logpath /data/db/mongod.log --fork –bind_ip 0.0.0.0

# MacOS - 自己下载安装
xcode-select --install
brew tap mongodb/brew
brew install mongodb-community@4.4 
# 本质上也是下载下面的文件Updating Homebrew...
==> Installing mongodb-community from mongodb/brew
==> Downloading https://fastdl.mongodb.org/tools/db/mongodb-database-tools-macos-x86_64-100.3.1.zip
==> Downloading https://fastdl.mongodb.org/osx/mongodb-macos-x86_64-4.4.5.tgz
==> Installing dependencies for mongodb/brew/mongodb-community: mongodb-database-tools
==> Installing mongodb/brew/mongodb-community dependency: mongodb-database-tools

# 如果有报错，```brew uninstall mongodb```之后再安装
brew services start mongodb/brew/mongodb-community

# 云部署
Atlas免费测试账号：
可以cloud.mongodb.com,注册登录之后就可以免费创建集群了（白名单ip+用户名密码）
然后用命令行连接集群
```

```
# 导入样本数据
curl -O -k https://raw.githubusercontent.com/tapdata/geektimemongodb-course/master/aggregation/dump.tar.gz
tar -xvf dump.tar.gz
mongorestore -h localhost:27017
```
