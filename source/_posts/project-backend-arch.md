---
title: project-backend-arch
date: 2024-04-23 15:13:52
tags:
---
- 监控：
ELK，dingtalk,grafana,prometheus,sentinel,sw,bonree

- 影子数据，影子库
- tidb kafka tdmq es redis mongo

- APP-tidb, DWS tidb, DWD tidb|kafka, ODS binlog|pv|kafka|burypoint|DB
- Flink | Tispark

- consul | nacos

- 一层网关

- 二层网关TO B，二层网关 To C

- ToB账号｜操作日志｜产品｜视频库｜录排｜题目｜文件｜搜索｜互动视频
- 学习｜账号｜复习｜作答｜推荐
- admin

```
在Java项目中，DWS, DWD, ODS这三个词通常用于数据仓库架构中：

1. ODS (Operational Data Store)：操作型数据存储层，它通常用于存储来自业务系统的原始数据，多用于业务运营分析。

2. DWD (Data Warehouse Detail)：数据仓库明细层，也被称为数据池层。在该层中，数据经过清洗、转换、集成等 ETL 操作后，形成数据仓库中的详细数据，主要为下一层 DWS 提供数据支持，多用于细粒度数据分析。

3. DWS (Data Warehouse Summary)：数据汇总层，也被称为数据仓库汇总层。在该层中，数据基于业务需求进行汇总操作，常用于为数据展示层提供统计的事实数据，比如数据报表，数据指标等。

上述三层分别处理不同阶段的数据。ODS 将面向各种源系统的多种结构的数据直接加载到数据仓库中。DWD则是在ODS的基础上，进行数据清洗及处理，形成统一的、结构化的详细数据模型。而DWS则是在DW层的基础上，对数据进行加工处理和汇总计算，以支持业务统计和决策分析。
```

### 后端使用技术方案
1. 系统采用技术springboot + mybatis + redis + tdmq + kafka作为应用服务架构
2. 采用ticdc + flink + tispark 处理离线应用数据
3. 采用HIVE，HDFS存储埋点数据

### 技术创新点
1. 基于腾讯云点播，支持交互式视频点播，支持与学生互动的学习形式。
2. 采用Hive技术，处理系统全埋点事件，方便分析用户学习使用情况。
3. 自研中间件，处理redis，mq，线程池，微服务等，为服务提供影子服务。
4. 基于网关+FLINK,利用ip和用户id，监控异常流量，提供风控预警服务