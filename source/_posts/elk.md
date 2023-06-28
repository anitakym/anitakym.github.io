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