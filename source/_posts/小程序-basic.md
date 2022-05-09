---
title: 小程序-basic
date: 2022-05-09 22:52:28
tags:
---


## 开发工具
- 代码提示
- 设置 - 编辑设置
- 真机调试 - 发给第三方（用户）
- 预览 - 自己用
- 详情 - 本地设置 - 看基本库版本

### 路由
- https://developers.weixin.qq.com/miniprogram/dev/api/route/wx.switchTab.html

### 组件｜接口
- 设计的边界

## 运行机制
- 热启动｜冷启动 - 缓存｜getupdateManager 
- 主动销毁 - 内存警告｜进入后台一定时间
- 前台状态｜后台状态

### 双线程架构
- why - 安全+管控
- View - 视图线程 && App Service - 逻辑线程
- View | App Service | Native
- view - Page(WXML|WXSS)
- App Sevice - Manager | API
- Native - 微信能力｜离线存储｜网络请求｜JSBridge
- Event | Data

#### setData
- evaluateJavaScript实现的(hybrid也是)
- （安卓）可能页面卡顿（界面滑动中 - 视图线程 - 渲染中）是由evaluateJavaScript导致的
-  逻辑层发来的请求阻塞了，阻塞超过200MS就会有卡顿的感觉
#### ios
- wkwebview - 内存紧张，wkwebview会被回收，所以一些历史页面我们回不去

#### wxs
- wxs不依赖于运行时的基础库版本 - 可以在所有小程序版本里面运行
- 运行在View线程里
- 提高View层运行效率
- 运行环境和其他JS代码是隔离的
- IOS上效率高，android上面和JS没啥差别
- 应用场景 - 如何提高效率

#### 视图线程
- 编译原理
- 小程序视图层是在polymer基础上，基于web component 标准实现的
- 类似Vue的实现
- 原生在vw上面
- 生命周期

#### 逻辑线程
- 初始化｜等待激活｜激活｜后台运行 - 四个状态

## wxss
- 选择器，不断发展中
- rpx
- 字体配置跟着系统走
- 小程序 app.wxss可以设置全局样式 - 字体等 - ```page { font-family: "xxx" }```
- 全局样式表里面设置的样式 - 可以被组件继承的 - font|color (见官方文档)
- 页面和组件的概念要分清楚
- 文件间距可以用line-height消除空白

## 事件
### tap
- bind:tap 一般不阻止点击事件的冒泡
- catch:tap

## 组件

### icon组件


### 自定义组件