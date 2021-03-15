---
title: chrome版本更新
date: 2021-03-15 15:34:37
tags:
    - chrome
---

今天测试老师report了一个在Chrome浏览器上的样式问题，排查了下，88无问题，89有问题 —— 具体查，某个没有用scoped的模块，/deep/的样式权重不够，直接被忽略了
让具体的开发老师处理了下代码，那为什么渲染会有差异呢，哪部分的处理变更了呢，查了下Chrome的更新文档

在Google直接搜索 web updates
https://developers.google.com/web/updates/2021
https://chromium.googlesource.com/chromium/src/+log/89.0.4389.72..89.0.4389.82?pretty=fuller&n=10000
https://developer.chrome.com/blog/deps-rems-89/

[Deprecation] /deep/ combinator is no longer supported in CSS dynamic profile.It is now effectively no-op, acting as if it were a descendant combinator. /deep/ combinator will be removed, and will be invalid at M65. You should remove it. See https://www.chromestatus.com/features/4964279606312960 for more details.


https://www.chromestatus.com/features#%2Fdeep%2F

https://segmentfault.com/a/1190000021576348

https://www.cnblogs.com/CyLee/p/10006065.html
