---
title: Java项目-startup
date: 2021-08-30 13:58:02
tags:
---

> 公司 Java 项目快速起起来，一是深入了解下架构和实现，二是方便本地起，做调试；能在对接具体问题的时候，具体脉络有个清晰的概念；

### 书籍 prepare

- 码出高效，阿里巴巴 Java 开发手册
- 编写高质量代码，改善 Java 程序的 151 个建议
- Google API design guide 中文版
- netty 权威指南

### Java 代码规范

- alibaba-代码规约 plugin
- findBugs - plugin
- SonarLint
- sequence diagram
- 设计原则：单一职责｜开闭｜接口隔离｜里氏替换｜迪米特｜依赖倒置

### 数据库设计规范

#### 命名规范

- 库｜表｜字段 名不允许出现大写字母
- 统一规范，数据库名：`ucan_业务名` ｜ 表名：`业务名_类型名_实体名`
- 表类型：tb（基础信息表-数据基本不会增长） | td（业务产生数据表-数据随着用户操作增长） | tr（业务关系表-实体间的关联关系表）
- 普通索引命名： `idx_字段名_字段名`； 唯一索引命名：`uniq_字段名_字段名`；

#### 设计规范

- 表｜字段 - 必须有注释
- 表间逻辑关系
- 表结构设计文档

#### 设计文档规范

- 项目背景（背景｜现状）
- 设计目标
- 系统设计（总体架构｜边界说明｜模块设计｜核心数据结构｜存储设计｜接口设计｜稳定性考虑｜兼容性考虑｜性能考虑）
- 测试关注点
- 上线及回滚方案
- 工作拆解

#### 运维部署文档

- 数据库｜缓存
- 域名
- git
- 服务器
- 服务器内项目地址｜文件夹权限｜日志地址｜ 日志索引
- 队列

### Tips

- 如果非结构化数据不涉及查询，聚合等操作，可以用 MySQL 的 JSON 字段替换 MongoDB document（分布式事务处理｜）

### rules
- 把简单的问题尽可能交给工具完成
- 简单
 - 1、代码格式化 包引用
 - 2、编码规范规约（安装阿里的代码规约插件），右键菜单点击编码规范扫描
 - 3、安装FindBugs插件，用FindBugs查找bug
 - 4、安装SonarLint插件，右键菜单选Analyze with SonarLint
 - 5、安装Sequence Diagram 插件，可以从controller层点右键查看调用路径
- 中等：1、根据模块业务查看代码逻辑，确认代码正确2、根据代码确认完成功能开发
- 复杂：查看代码符合的设计原则，是否符合整体架构逻辑【原则是复杂的问题简单化】设计原则：单一职责、开闭、接口隔离、里氏替换、迪米特、依赖倒置


### Java API Design Best Practices
- https://static001.geekbang.org/con/33/pdf/3939125782/file/1%E3%80%81jgiles+-+API+Best+Practices+-+v2+-+qcon.pdf
- Jonathan Giles
- API design theory | practical advice
- effective java 3rd edition - joshua bloch
- API - 开发者 - 达成目标
- 抽象层面 - 更好的抽象
- API的使用者 ｜ 使用者的目的
- API Characteristics
 - Understandable
  - 使用者能看了能马上知道这个接口干什么的, 接口文档也是必须的
  - 面向对象的设计
  - entry points
 - Consistency
  - null 的处理要严格符合文档里面写的
- restrained
- evolvable
- documentation
- there is no magical process to api Design
- api design is an art , and like art, becomes easier with practice


### APIs are the thing that gets us to the thing
- "Computers aren't the thing. They’re the thing that gets you to the thing."
 -- Joe MacMillan (Halt and Catch Fire)
- We have always assumed that applications are the thing
- The real “thing” is delivering solutions through capabilities
- APIs will always be a thing


## 线上项目debug
- arthas
```
2022-05-11 16:52:53.396 ERROR http-nio-8188-exec-26 com.xx.xxx.account.util.JwtUtil (JwtUtil.java:40)-
io.jsonwebtoken.ExpiredJwtException: JWT expired at 2022-04-30T09:41:22Z. Current time: 2022-05-11T16:52:53Z, a difference of 976291396 milliseconds.  Allowed clock skew: 0 milliseconds.
at io.jsonwebtoken.impl.DefaultJwtParser.parse(DefaultJwtParser.java:385)
```
- http://arthas.gitee.io/
- https://github.com/alibaba/arthas