---
title: HTTP相关问题
date: 2020-08-11 18:43:51
tags:
  - HTTP
---


#### 502网关问题
#### 415（unsupported media type）（content-type）
415 Unsupported Media Type 是一种HTTP协议的错误状态代码，表示服务器由于不支持其有效载荷的格式，从而拒绝接受客户端的请求。

格式问题的出现有可能源于客户端在 Content-Type 或 Content-Encoding 首部中指定的格式，也可能源于直接对负载数据进行检测的结果。

Java

500 内部报错

#### 503 service unavailable

服务端错误状态码，表示服务器尚未处于可以接受请求的状态

通常造成这种情况的原因是由于服务器停机维护或者已超载。注意在发送该响应的时候，应该同时发送一个对用户友好的页面来解释问题发生的原因。该种响应应该用于临时状况下，与之同时，在可行的情况下，应该在 Retry-After 首部字段中包含服务恢复的预期时间。
缓存相关的首部在与该响应一同发送时应该小心使用，因为 503 状态码通常应用于临时状况下，而此类响应一般不应该进行缓存。

cite(https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/503)
