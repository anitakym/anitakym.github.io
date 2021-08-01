---
title: whistle-基于node实现的跨平台抓包调试代理工具
date: 2021-03-02 10:11:41
tags:
    - node
---

### 应用场景
- 开发环境下，截图图片资源调试时，跨域的问题（也可在本地起nginx代理）
- 抓包配置交接问题

### Start UP
- [操作文档指南](http://wproxy.org/whistle/install.html)

> 来点简单的
```
npm i -g whistle
w2 -h
w2 start
```

### whistle代码分析


### nohost
- 基于whistle
- [nohost接入文档及github链接](https://nohosts.github.io/nohost/)

### Others
- nginx本地起代理解决跨域问题


## 应用场景
### CASE1-前端域名代理
#### 本地代理静态资源服务，用*.xdf.cn的域名即可
- 安装whistle，起whistle服务
```
  npm i -g whistle // 安装whistle
  w2 start // 起whistle
```
- 浏览器设置SwitchyOmega
```
chrome://extensions/ 
安装Proxy SwitchOmega，并进行配置
情景模式-新增一个叫whistle的，配置如图，配置完点击应用选项

![](redis-node.png)

在插件栏，选择上我们刚刚配置到情景模式
![](redis-node-2.png)


打开http://127.0.0.1:8899/，配置规则
选择 rules, 配置规则 127.0.0.1:8886 test.imagining.cn
然后点击 save 按钮

本地起完npm run dev 之后，浏览器输入 test.imagining.cn 即可访问本地

- auto switch 
可以这边进行配置，处理代理之间的切换

- https
打开http://127.0.0.1:8899/
点击https
打开"capture tunnel connects"选项

信任证书：
双击下载的证书，选择始终信任

重启W2:
w2 stop
w2 start
```