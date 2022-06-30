---
title: typescript-and-graphql
date: 2022-06-13 13:58:53
tags:
---
### 如果缺少类型校验，比较危险的场景
```
- fetch('/api/*')
从客户端发送到API的payload
从API返回给客户端的payload
- sql.query('SELECT * from things') (或其他类似的东西)
发送给数据库的query
从数据库返回给API的result set
```

### 携程基于GraphQL的BFF实践
https://mp.weixin.qq.com/s/q05JeUZ0mfjhhCshhhPNtw