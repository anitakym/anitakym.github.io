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