---
title: yuque桌面端分析
date: 2021-09-22 17:34:19
tags:
---
> 看语雀也用electron包了个桌面端，和我们这边现有的几款electron的application处理方式比较相似，稍微查看学习下；

### 分析方式
- 抓包（Charles）
- 反解（asar）
```
code Content
# 打开终端
cd resources
asar e app.asar app
# 这个时候，目录下就有了app文件夹，我们就可以具体看看了
# 目前结构清晰，代码是压缩编译过的，不影响看
# 找到main.js，加上
webContents.openDevTools()
# 重新启动客户端，调试工具就加上了
# 这个时候我们就能看到resources部分，资源大概是怎么分配的了，什么放在端上，什么不是
```

#### 包地址
- https://www.yuque.com/install/desktop

