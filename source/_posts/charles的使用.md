---
title: charles的使用
date: 2020-08-06 15:46:07
tags:
    - 工具篇
---

#### 官方文档指路
https://www.charlesproxy.com/documentation/
阅读指南：内容本身是比较简单的，如果需要的话，可以安装chrome 的 Google 翻译插件，点击翻译此页面，整个文档就被翻译了（需要开代理，不然可能用不了）
#### 问题解决
1. charles 突然打开就是一片空白

这个时候把电脑的shadowsocks代理给关掉了就好了


2. 怎么修改请求

在需要拦截的请求上面右击，选择breakpoints，再次抓到请求的时候，就会拦截，这个时候可以修改请求了（request， response都能改，先抓到的是options，然后是post请求）
（cmd + shift +4 截屏）


按Execute就会继续往下走


3. 配置APP预发环境测试的请求抓取

为了解决跨域问题，需要做下面的配置
![](charles1.png)

- Rewrite Settings
    - enable rewrites
- Rewrite Rules
    - Modify Header(Access-Control-Allow-Headers)
    - Remove Header(Access-Control-Allow-Origin)

```
Access-Control-Allow-Headers
Origin, Content-Type, Cookie, X-CSRF-TOKEN, Accept, Authorization, X-XSRF-TOKEN, Origin, Content-Type, Cookie, X-CSRF-TOKEN, Accept, Authorization, X-XSRF-TOKEN,currentStudentCode
```





















https://www.jianshu.com/p/75126f57e933

具体手机端的配置见上面链接里面的文档
















