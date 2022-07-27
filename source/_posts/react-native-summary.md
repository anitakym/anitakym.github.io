---
title: react-native-summary
date: 2021-10-25 23:39:14
tags:
---

> notion 2022-7.22 除编辑器部分，切回原生开发（这种重交互的应用，长期看来，性能是核心指标）
- 2020 rn 20-22 kotlin/swift + webview 22.7->从webview逐渐切回到原生
- https://www.notion.so/releases/2022-07-20
- https://twitter.com/jitl/status/1530326516013342723?s=20&t=xT0gfWhFvs0yNvc1GQ3sTQ
- https://mp.weixin.qq.com/s/Jzqx3DWLlowszESQfBJZ9A （搞不定移动端性能，全球爆火的Notion从Hybrid转向了Native）

## concept
### view为中心


## basic
- create
- run-ios | run android
- import

## 

## 直播
### preview view
### player view
 
### RN API
#### API设计风格
#### 配置管理
#### 状态管理
#### 动作管理
#### 事件管理


### RN Layout
- Flex Box
- Streaming View Hierarchy
 - AspectFrameLayout
 - CameraPreviewFrameView
 - GLSurfaceView
 - Focus View

### 腾讯云互动直播
- https://cloud.tencent.com/solution/ilvb

## 原生端和JS的通信
- JavaScriptCore 桥阶层 - 翻译
- RN对通信做了封装

### 从RN向JS传递原生信息
- 调用原生模块获取信息
- 页面初始props
- 原生端发送事件进行信息传递
- 原生端设置JS全局变量

```
通信效率 | 时机问题 | 多入口场景 | 影响调试
```

### JavaScriptCore


## Core - Basic 
### Component


### Style


### State
- state - page里面会“动”的数据
- state - 初选 ｜ 确定 ｜ 声明 ｜ 更新
- 一件事情一个状态 & 重复状态去除 & 可计算的不是新状态


### fast refresh
- 快速刷新 => https://reactnative.dev/blog/2019/09/18/version-0.61#fast-refresh
- `{} !== {}`
- 基础的模块替换功能 - 组件级别的强制刷新
- 复用组件和状态
 - 编译时-修改组件的注册方式
 - 运行时-“代理”的方式管理新旧组件的切换
 - 
