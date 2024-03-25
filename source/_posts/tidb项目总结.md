---
title: tidb项目总结
date: 2021-11-09 17:17:44
tags:
---
## 官方文档指路
- https://github.com/pingcap/tidb
- https://docs.pingcap.com/zh/tidb/stable



## Tips

### properties
#### max-server-connections
- https://docs.pingcap.com/zh/tidb/stable/tidb-configuration-file#max-server-connections
- 用来兼容mysql协议的一个参数
```
- TiDB 中同时允许的最大客户端连接数，用于资源控制。
- 默认值：0
- 默认情况下，TiDB 不限制客户端连接数。当本配置项的值大于 0 且客户端连接数到达此值时，TiDB 服务端将会拒绝新的客户端连接。
```

### 问题现象
TiDB事务失效
背景
xxx只连了TiDB
新需求增加了Mongo，增加了Mongo的数据库配置
原因
Mongo的也配置是事务管理，与TiDB的事务管理冲突，导致事务失效