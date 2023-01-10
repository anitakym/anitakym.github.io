---
title: 客户端缓存-redis6
date: 2021-07-05 15:19:55
tags:
---

### 参考文章
- http://antirez.com/news/130
- https://redis.io/topics/client-side-caching
- https://www.youtube.com/watch?v=kliQLwSikO4
- https://www.slideshare.net/RedisLabs/redisconf18-techniques-for-synchronizing-inmemory-caches-with-redis
- https://mp.weixin.qq.com/s/4hpu4R-IG3CgLTi_U7rjig

#### 6.0 + feature
- 实现了服务端协助的客户端缓存功能 - tracking
- 作用
  - 普通模式
  - 广播模式
  - 重定向模式
- 场景 -> 加速业务应用访问


## 6.0 others feature
- 面向网络处理 - 多IO线程
- 细粒度的权限控制
- RESP 3 协议