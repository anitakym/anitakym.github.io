---
title: elk
date: 2020-11-11 12:00:13
tags:
---
## kibana query-string-Syntax
### doc
- 过滤器语法基于Lucene
- elastic文档
- https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html#query-string-syntax
- lucene语法
- https://lucene.apache.org/core/6_6_0/queryparser/org/apache/lucene/queryparser/classic/package-summary.html
- 引导demo
- https://demo.elastic.co/cookie/index.html#/discover

## filebeat配置

- https://github.com/elastic/beats - The Beats are lightweight data shippers, written in Go
- logstash-forwarder - THIS PROJECT IS REPLACED BY FILEBEAT(6年前，Commits on Nov 13, 2015)
- filebeat - https://www.elastic.co/guide/en/beats/filebeat/current/index.html
- https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-overview.html

### 问题
- 日志不活跃，filebeat关闭连接
- filebeat配置有问题，导致收集路径错了，修改配置，重启下，索引创建，就能看到日志了

## LogStash
- https://github.com/elastic/logstash
- Logstash is part of the Elastic Stack along with Beats, Elasticsearch and Kibana. Logstash is a server-side data processing pipeline that ingests data from a multitude of sources simultaneously, transforms it, and then sends it to your favorite "stash." (Ours is Elasticsearch, naturally.). Logstash has over 200 plugins, and you can write your own very easily as well.

#### 配置


## CKafka
- https://cloud.tencent.com/document/product/597/32743

## keyword
https://www.elastic.co/guide/en/elasticsearch/reference/6.7/query-dsl-query-string-query.html#query-dsl-query-string-query

devtools
GET xxx/_mapping
可以看keyword抓取的字符数限制

## 聚合搜索
- inspect 查看搜索具体语句
- dev-tools 粘贴刚刚的语句，进行aggs的修改
```
"size": 0,
  "aggs": {
    "orders_by_ip": {
      "terms": {
        "field": "client_ip.keyword"
      }
    }
  },
```
-- 或者可以用visualize , 选择已保存的语句，buckets里面add aggs

## words
### elasticsearch
Elasticsearch是一个开源的分布式搜索和分析引擎，适用于所有类型的数据，包括文本、数字、地理位置、结构化和非结构化数据。Elasticsearch在复杂搜索场景下表现出色，这主要归功于其对全文搜索的强大支持，这是它作为Apache Lucene库的扩展而获得的。

Elasticsearch的主要特点包括：

1. 分布式和高可用性：Elasticsearch自动处理数据的分片和副本，以支持扩展和容错。

2. 全文搜索：Elasticsearch提供了强大的全文搜索能力，支持多种语言。

3. 实时分析：Elasticsearch可以在大规模数据上进行近实时的复杂查询以提供实时分析。

4. 可扩展性：Elasticsearch可以水平扩展到上百台服务器，处理PB级别的数据。

Elasticsearch常用于以下场景：

- 网站搜索：为网站提供复杂的搜索功能，如全文搜索、模糊搜索、同义词搜索等。
- 日志和事务数据分析：收集、分析和可视化日志或事务数据。
- 安全情报：收集、分析和可视化安全事件数据。
- 商业智能：对大量数据进行实时分析，提供即时的商业洞察。

Elasticsearch也是ELK（Elasticsearch、Logstash、Kibana）堆栈的核心组件，这是一种广泛使用的开源日志分析解决方案。

### logstash
Logstash是一个开源的数据收集引擎，它具有实时管道能力。Logstash可以动态地从各种来源收集数据，并将其转换和发送到你选择的存储/分析目标。

以下是Logstash的一些主要特性：

1. 插件化：Logstash支持大量的插件，可以从各种数据源中提取数据，包括日志文件、系统指标、网络设备等。

2. 实时处理：Logstash可以实时处理和转换数据，这对于需要实时分析和反馈的应用场景非常有用。

3. 数据过滤和转换：Logstash提供了丰富的过滤器插件，可以对数据进行各种处理，包括解析、转换、添加和删除字段等。

4. 与Elasticsearch和Kibana的集成：Logstash是Elastic Stack的一部分，可以与Elasticsearch和Kibana无缝集成，提供强大的搜索和数据可视化能力。

应用场景包括但不限于：日志和事件数据管理，IT运维，安全分析，业务分析等。

### Kibana
是一个开源的数据可视化和探索平台，设计用于与Elasticsearch协同工作。它提供了一种在Elasticsearch索引中导航和查找数据的用户友好的界面。Kibana让大量数据更易于理解，它的简单、基于浏览器的界面使你能够快速创建和共享动态仪表板，显示Elasticsearch查询的变化。

Kibana的主要功能包括：

1. 数据搜索：可以对Elasticsearch中的数据进行搜索和查询，支持Lucene查询语法。

2. 数据可视化：可以创建各种类型的图表，如柱状图、线图、饼图等，以直观地展示数据。

3. 仪表板：可以将创建的图表组合成仪表板，用于数据监控和业务分析。

4. 地图：可以在地图上展示地理位置数据，支持地理空间分析。

5. 时间线分析：可以对时间序列数据进行分析，用于日志和事件数据分析。

6. 机器学习：可以使用Elasticsearch的机器学习功能，对数据进行异常检测和预测。

Kibana广泛应用于日志和事件数据分析、实时应用监控、搜索行为分析等场景。


### 一个完整的集中日志管理系统需要包括以下主要功能：

收集：可以从各种来源收集日志信息。
传输：可以稳定地将日志数据传输到日志系统。
存储：如何存储日志数据。
分析：可以支持UI分析。
警告：可以提供错误报告和监控机制。


### 
- 一般情况下，使用ELK技术栈搭建日志中心时，只需部署单体的ELK技术栈即可。整套部署下来，也只需要一个Logstash实例、一个Elastic Search实例和一个Kibana实例，
- 业务线较多，且系统体量大，日志量增多，可以在单体部署的基础上进行优化。比如部署多个Logstash实例，Elastic Search也采用集群部署的形式
- 搭建ELK日志中心“究极体”的话，可以引入FileBeat组件和Kafka消息队列。Logstash组件则只作为日志过滤的工具，把日志采集流程交给FileBeat组件，Kafka则用于削峰填谷，减轻日志中心在数据采集时的压力。同时，各组件在搭建时都需要进行分布式部署或者集群部署，如下图所示，而这就是非常重的日志中心搭建方式，所支撑的业务线和日志量就非常大了。