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


## rn - lib
- 可腾讯云文档里面搜，他们支持的sdk
- bonree也支持
#### .podspec
- CocoaPods


### ENV SETUP
#### watchman
- brew install watchman
- Facebook Watchman 是一个文件监视服务，用于监控文件系统的更改。对于 React Native 项目，Watchman 可以提高开发效率，因为它能够实时监控项目中的文件更改并自动重新构建和刷新。当文件发生更改时，它会在后台执行相应的任务，例如实时重新加载应用。

#### ruby
- Ruby是一种通用的编程语言。React Native在一些与iOS依赖性管理相关的脚本中使用。和每一种编程语言一样，Ruby也有不同的版本，这些年来一直在开发。
- React Native使用一个.ruby-version文件来确保你的Ruby版本与需要的版本相一致
- ruby --version
- 一些常见的Ruby版本管理器是：
```
rbenv
RVM - https://rvm.io/
chruby
带有asdf-ruby插件的asdf-vm
```
- .ruby-version 

### CLI
- React Native有一个内置的命令行界面。与其在全局范围内安装和管理特定版本的CLI，我们建议你在运行时使用Node.js附带的npx来访问当前版本。使用npx react-native <command>，当前稳定版本的CLI将在运行命令时被下载和执行。

### metro
Metro 是一款由 Facebook 开发的自动化打包器和优化器，用于加速 React Native 和 Node.js 的开发。Metro 不仅在 Facebook 得到了广泛应用，还在其他很多公司和开源项目中使用。一些使用 Metro 的知名案例包括：

Walmart：全球最大的零售商之一，使用 Metro 优化其 React Native 应用程序。
Expo：提供了一个从头开始开发 React Native 应用程序的工具套件，内部使用了 Metro。
Callstack：专门从事 React Native 项目开发的 IT 公司，使用 Metro 作为其优化器和打包器。
Wix：为其 React Native 应用程序使用 Metro 进行打包和优化。
Microsoft: 使用 Metro 作为其 React Native for Windows 和 React Native for macOS 项目的一部分。
#### 构建阶段
- Resolution：此阶段Metro会从入口文件出发分析所依赖的模块生成一个所有模块的依赖图，主要是使用jest-haste-map这个包做依赖分析。这个阶段和Transformation阶段是并行的；
- Transformation：此阶段主要是将模块代码转换成目标平台可识别的格式；
- Serialization：此阶段主要是将Transform后的模块进行序列化，然后组合这些模块生成一个或多个Bundle
### cases
#### React Native工程Monorepo改造实践
- https://juejin.cn/post/7177585131861835837
#### 基于 React Native 的动态列表方案探索
- https://juejin.cn/post/7142819695840722975