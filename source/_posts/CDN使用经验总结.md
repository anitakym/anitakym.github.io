---
title: CDN使用经验总结
date: 2021-03-19 11:53:42
tags:
---
项目经验：
私有CDN部署格式：
可参考：https://www.jsdelivr.com/package/npm/vue?version=3.0.7
load下来包以后，取目录，然后部署

参考文档：
https://blog.bitsrc.io/boost-frontend-load-speed-using-cdn-7ae02cbbf492

- 静态资源如果做了CDN加速，注意CDN缓存问题，如果更新了同名资源，要主动刷新缓存！！
- 我们这边是在CI中配置了刷新的流程，上完线主动刷新(针对有同名资源的情况，如果项目本身只有index.html是名称不变，别的资源名都有内容hash，则可以不同刷新，直接在CDN缓存策略里面配置index.html的规则即可)
- 对于资源部分，通知运维进行主动刷新


### 腾讯云
x-cache-lookup: cache hit
x-cache-lookup: hit from inner cluster
- 命中
x-cache-lookup：hit from upstream
- 未命中

