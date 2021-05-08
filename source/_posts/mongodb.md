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
- 中文版手册-https://docs.mongoing.com/

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

#### 闲话
- 竞品：
14年，微软推出了DocumentDB预览版，17年5月升级为Cosmos DB（包含多个数据模型，文档模型成为子集）
MongoDB-易用性！ 稳定性（丢数据，安全，分布式处理能力）？
DocumentDB-Leslie Lamport(对事务的处理，自动索引，PaaS服务)
做成了Windows Azure的一个服务
17年，提供了兼容MongoDB的API
（17年1月，黑客大量袭击了默认安装的MongoDB）

- 人
DoubleCLick原创始人（Dwight Merriman, Kevin Ryan, Eliot Horowitz）
原先想做一个云计算的服务的
然后先搭一个数据库

mongo - humongous - 海量数据库 - 面向集合，模式自由，文档型数据库（Accelerate development, address diverse data sets, and adapt quickly to change with a proven application data platform built around the database most wanted by developers 4 years running.）

PS：SQL是IBM出来的

10gen 在 2009年2月正式开源MongoDB的第一个版本

商业上-资助用户组，对社区的支持，技术支持团队-nice（用户体验）

13年更名 MongoDB公司



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

# centos - 本地安装
# 新建一个/etc/yum.repos.d/mongodb-org-4.2.repo，这样我们可以用yum来安装
[mongodb-org-4.2]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.2/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.2.asc

# 然后安装最近的稳定版本
sudo yum install -y mongodb-org

# 启动社区版
# 默认会在/var/lib/mongo(data) /var/log/mongodb(log)，如果想要改到自己创建的目录，可以修改/etc/mongod.conf文件
sudo chown -R mongod:mongod <directory> # 注意权限问题

# 看用systemctl（较新版本Linux） 还是 service （较老版本），可以用"ps --no-headers -o comm 1"查，我这边centos7，用的是systemctl
systemctl start mongod

# 如果报错“Failed to start mongod.service: Unit mongod.service not found.”
systemctl daemon-reload

# 查看是否成功启动
systemctl status mongod

# 如果想随着系统reboot开启
systemctl enable mongod

# 关
systemctl stop mongod

# 重启
systemctl restart mongod

# 使用
mongo

# MacOS - 自己下载安装
# https://docs.mongoing.com/install-mongodb/install-mongodb-community-edition/install-on-macos
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
# mongorestore 
curl -O -k https://xxx.xxx.com/dump.tar.gz
tar -xvf dump.tar.gz
mongorestore /dump
```

### 查看工具
- mongoDB compass(官方，免费，好用)
- studio3T
- NoSQL Booster

grafana:
https://grafana.com/grafana/dashboards/8339