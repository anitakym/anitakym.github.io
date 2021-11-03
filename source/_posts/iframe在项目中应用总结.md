---
title: iframe在项目中应用总结
date: 2021-09-22 18:28:21
tags:
---
### 已落地的多种项目形式
- 富文本编辑器-结合业务的输出
- 公式编辑器

### 跨部门团队协作
- XXX-客户端，嵌入iframe
- 报告对接
- 中台系统-业务模块输出

### 什么时候用？怎么用？

## 基础点
### iframe
- https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/iframe

### hack
- 基于iframe的src,提供下载资源功能
### 通信
#### postMessage
- https://developer.mozilla.org/zh-CN/docs/Web/API/Window/postMessage

### 线上问题处理
#### CSP
- https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
- Specifies valid parents that may embed a page using <frame>, <iframe>, <object>, <embed>, or <applet>

```
# 不允许被嵌入
Content-Security-Policy: frame-ancestors 'none'
# 只允许被同源的页面嵌入
Content-Security-Policy: frame-ancestors 'self'
# 只允许被白名单内的页面嵌入
Content-Security-Policy: frame-ancestors www.example.com

# 不允许被嵌入
X-Frame-Options: deny
# 只允许被同源的页面嵌入
X-Frame-Options: sameorigin

```

### nginx
如果一个域名xxx.xxx.xxx  /abc/ 路径下部署了前端服务

- iframe 里面嵌入 xxx.xxx.xxx/abc
- 如果是xxx.xxx.xxx/abc 会被重定向，nginx , 这样会有问题，请求https，会被转为http
- Nginx 内部重定向规则会被启动，例如，当 URL 指向一个目录并且在最后没有包含“/”时，Nginx 内部会自动的做一个 301 重定向
- 需要xxx.xxx.xxx/abc/ ，这样才能匹配到，从而不被重定向
