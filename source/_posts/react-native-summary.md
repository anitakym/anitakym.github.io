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
Watchman主要依赖几种主要的库和软件，这些库和软件包括：
1. Autoconf：一个用于自动化生成可移植编译系统的工具，它会根据你的系统环境和你的特定需要来生成一份适合你机器的Makefile。
2. Automake：与Autoconf配套使用的工具，它可以自动产生跨平台的Makefile.in文件。
3. Libtool：用于创建可移植库的工具。
4. pkg-config：它是用来在配置阶段检测库安装路径的工具。当你编译需要一些库文件（比如X、GTK、QT库等）支持的程序时，你可以用它快速找到这些库文件安装在哪里。
5. Python-dev (仅在构建Python扩展时需要)
6. OpenSSL (仅在构建fb303 Thrift 服务时需要)

Zstandard（也被称为zstd）是一个实时压缩算法，提供高压缩率和极快的解压缩速度。它由Facebook开发并且已经开源。Zstandard在设计上十分灵活，可允许用户在压缩/解压缩速度与压缩率之间进行权衡。
1. 高性能：它提供了类似gzip的压缩率，但解压速度要快得多，对于需要频繁解压缩的场景，比如服务端服务，效果明显。
2. 高压缩比：Zstandard也支持高压缩等级，以获取更高的压缩比，这意味着它可以为需要压缩大量数据的场景，如数据仓库大规模存储和传输，提供更好的解决方案。
3. 具备字典压缩功能：Zstandard可以训练一个字典，以改进小数据压缩。如果存在大量的重复字符串，使用预训练的字典可以显著提高压缩率。
在大多数系统上安装zstd非常简单，对于Unix/Linux系统，可以通过包管理器(如apt, yum等)来安装。例如，在基于Debian的系统上，可以用以下命令安装：
```bash
sudo apt-get install zstd
```
在macOS上，你可以通过brew来安装：
```bash
brew install zstd
```


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

###
- https://github.com/microsoft/react-native-windows

- apps - opensource
https://github.com/ReactNativeNews/React-Native-Apps