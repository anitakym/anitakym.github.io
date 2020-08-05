---
title: Windows10分享文件到Mac
date: 2018-09-14 17:11:28
tags: 
    - 很久以前系列
---
> 因为想把有道云笔记迁移到notability上，但是有道云笔记只支持在PC客户端进行全部导出到操作，所以需要从PC快速分享文件到Mac上
#### 方法
首先保证windows电脑和Mac 在同一局域网
- window上： 运行-> cmd -> ifconfig -> 得到本机在局域网到ip
- window上： 右键文件夹-> 属性 ->共享-> 高级 -> 共享此文件夹 -> 确定
- Mac 上: 在 Finder 到前往里面选择’连接服务器’, 输入 smb://10.200.170.52（你获得的windows电脑的ip）,点连接， 然后输入windows的管理员的名称和密码即可（在windows的设置->账户信息里面可以查到）。