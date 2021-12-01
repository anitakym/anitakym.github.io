---
title: browser相关-一些总结
date: 2021-09-17 16:47:43
tags:
---

###
- https://www.html5rocks.com/zh/tutorials/internals/howbrowserswork/
- loupe
### DTD



## 问题处理
### 清除所有cookie相关
同样项目，起本地前端服务调试的时候，一个同事的电脑请求返回如下
```
{"status":0,"message":"com.google.gson.stream.MalformedJsonException: Unterminated string at line 1 column 7 path $.","data":null}

```
清除了浏览器的所有application里面cookies等缓存，再次请求就好了

服务端日志是入参被截断了；