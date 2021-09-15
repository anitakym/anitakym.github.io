---
title: dns-prefetch
date: 2021-09-15 14:56:53
tags:
---
> 之前对同一个系统的不同端及业务做了域的划分，切了不同的域名；降低服务器的压力；
> 外网域名都会先走集团的服务
> 目前会有几个移动端的项目，静态资源域本身会做CDN加速，然后入口页会集成不同业务，在合适的场景下，做下DNS-prefetch

### 文档指路
- https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/X-DNS-Prefetch-Control

### 检测方式
- WebPageTest
- https://www.webpagetest.org/
- 可以看到DNS解析消耗的时间

### 原理
- 通过html里面增加meta,告知浏览器，先解析指定链接，提前查询
- 缓存DNS查询结果

### 适用情况
```
chore:根据使用场景，增加DNS-Prefetch，项目负责人后续可根据业务及首页拉取情况进行增加或者删减(如果首屏不请求，后续会请求，且业务场景多的，可增加；如果首屏已请求，则可删除，避免浪费)

    <!-- add dns-prefetch according to situation, if have been fetched in fisrtpage, just delete it; -->
    <meta http-equiv="x-dns-prefetch-control" content="on" />
    <link rel="dns-prefetch" href="//xxx.xxx.cn" />
    <link rel="dns-prefetch" href="//xxx.xxx.cn" />

```

### 使用方式
```
# 打开和关闭 DNS 预读取
X-DNS-Prefetch-Control: on
X-DNS-Prefetch-Control: off

<meta http-equiv="x-dns-prefetch-control" content="off">
# 强制查询特定主机名
<link rel="dns-prefetch" href="http://www.spreadfirefox.com/">

```

### 注意
不要滥用，否则会增加DNS的压力（基于逻辑和数据来判断使用的场景和具体域）
感觉最合适的应该是国际化的站点，如果没有对应国家部署不同的域的话；