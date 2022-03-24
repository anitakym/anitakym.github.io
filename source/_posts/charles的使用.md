---
title: charles的使用
date: 2020-03-11 15:46:07
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


#### 基本原理-手机端
Charles - 代理软件 - SSL/流量控制/重发，修改请求等
> 手机通过电脑进行网络访问，因而，电脑的host设置，对手机的请求也有效（移动端配置host要root权限）；离线发布时候，可以把请求直接映射到某个服务器

- 手机和电脑同一网络环境
- Charles - proxy - proxy settings - proxies 
- 勾选 enable transparent http poxying ， 端口号设置
- 手机代理设置： 端口号和电脑设置的保持一致


#### https请求抓取
- 原理，Charles对客户端伪装成服务器，对服务器伪装成客户端
- Help -> 添加Charles的根证书
设备上下载完证书，点击证书，如果提示到设置里面安装，则可以在设置里面全局搜索：“证书”｜“安装证书”，就可以找到安装的地方了；
- 问题解决：https://blog.csdn.net/liushaofang/article/details/106421834


#### host
- Tools 
- Map Remote Settings
- 选择enable map remote
- Add 
- (记得选择 Preserve host in header fields)
```
502 Bad Gateway
The proxy server received an invalid response from an upstream server. Sorry for the inconvenience.
Please report this message and include the following information to us.
Thank you very much!
如果不选择，会有相关报错
```






