---
title: puppeteer-node-pdf-service
date: 2021-03-19 16:30:34
tags:
---
不涉及业务，讲一下技术方面PDF生成服务的心得

### 文档指北：
- puppeteer(https://github.com/puppeteer/puppeteer)
<pre>
Puppeteer is a Node library which provides a high-level API to control Chrome or Chromium over the DevTools Protocol. Puppeteer runs headless by default, but can be configured to run full (non-headless) Chrome or Chromium.
</pre>

应用场景：
1. 页面截图服务
2. PDF生成服务
3. 自动化测试
4. 服务端渲染内容抓取

try:https://try-puppeteer.appspot.com/

就几乎碰到的问题，文档上面都能找到，所以文档和生态还是比较完备的
https://github.com/puppeteer/puppeteer/blob/main/docs/api.md


也有troubleShooting的文档：
https://github.com/puppeteer/puppeteer/blob/main/docs/troubleshooting.md

## History

### 几次技术改造

- downloadCenter
- 从接口获取模版渲染数据 -> 从mongodb获取
- XX_report 进度状态原先由接口返回 -> 返回到mq
- node服务本身 - 配合修改+日志+调试配置开关


### 部署和CI优化
#### 底层脚本
- pm2配置
```
```

#### Jenkins可视化集成