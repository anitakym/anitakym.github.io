---
title: httpVersion-summary
date: 2022-12-09 16:11:21
tags:
---
- http://www.alloyteam.com/2016/07/httphttp2-0spdyhttps-reading-this-is-enough/
```
cite: 
对比 HTTPS 的升级改造，HTTP2.0 或许会稍微简单一些，你可能需要关注以下问题：

前文说了 HTTP2.0 其实可以支持非 HTTPS 的，但是现在主流的浏览器像 chrome，firefox 表示还是只支持基于 TLS 部署的 HTTP2.0 协议，所以要想升级成 HTTP2.0 还是先升级 HTTPS 为好。
当你的网站已经升级 HTTPS 之后，那么升级 HTTP2.0 就简单很多，如果你使用 NGINX，只要在配置文件中启动相应的协议就可以了，可以参考 NGINX 白皮书，NGINX 配置 HTTP2.0 官方指南。
使用了 HTTP2.0 那么，原本的 HTTP1.x 怎么办，这个问题其实不用担心，HTTP2.0 完全兼容 HTTP1.x 的语义，对于不支持 HTTP2.0 的浏览器，NGINX 会自动向下兼容的。
```
- https://http2.akamai.com/
```
https://caniuse.com/?search=http2
http://www.alloyteam.com/2015/03/http2-0-di-qi-miao-ri-chang/
```
- https://http3-explained.haxx.se/zh


- https://cloud.tencent.com/developer/article/1464264

### 腾讯云点播

- 腾讯云点播，如果想支持http2.0，发下需要配置的域名，腾讯云点播后台来配置就行，有个变更窗口了，需要下周一才能配置

- 配置之后，就会支持http2.0

- head of lin blocking - 对同一个域下请求数量的限制 - 2.0 基于二进制分帧，可避免这个问题

- 影响绝大多数应用性能的并非带宽，而是延迟，而2.0能解决这个问题； 我们这边云点播就出现用户反馈，观看卡顿，用腾讯云的华佗测速工具，发现延迟较大，带宽是OK的；

### 腾讯云CDN
- https://cloud.tencent.com/document/product/228/41689
```
HTTP2.0 作为最新的 HTTP 协议，大幅提升了 Web 性能，进一步减少了网络延迟。已配置证书启用 HTTPS 加速的域名，可自助开启 HTTP2.0 协议支持。
注意：
目前仅支持 HTTP2.0 访问，暂不支持 HTTP2.0 协议回源。
（"回源"是网络技术中的术语，主要在CDN（内容分发网络）技术中使用。回源是指当CDN的边缘节点收到用户请求时，如果节点没有请求的内容，那么这个节点就需要向原服务器（源站）请求这个内容的过程，这个过程就叫“回源”。

一般来说，在CDN中，用户的请求首先会被指向最近的边缘节点。如果这个节点有用户请求的内容（比如网页、图片、视频等），那么就直接从这个节点把内容提供给用户。这样可以大大提高用户访问的速度，因为内容的传输距离变短了。

但是，如果这个边缘节点没有用户请求的内容，那么它就需要向原服务器（源站）请求这个内容。源站把内容返回给边缘节点，节点再把内容提供给用户，这个过程就是“回源”。

"回源"的过程对于CDN服务提供商来说，需要消耗较高的带宽和资源，因此通常会尽量通过缓存等技术，减少回源的发生。）
```
- CDN - 把数据放到离用户地理位置更近的地方，减少每次TCP连接的网络延迟，增大吞吐量

### 推荐书
- web性能权威指南 - qq阅读上面有，可当工具书查看使用

### http 基础
#### 数据传输
- url param
- query
- form-urlencoded
- form-data
- json

### 项目数据
- 先升了腾讯云点播的域名(支持http2.0)
- xxxvod.xxx.cn