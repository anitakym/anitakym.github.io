---
title: flutter-study-summary
date: 2021-09-25 17:09:52
tags:
---
# Part1 - 领域knowledge

## Dart
### Tools
- Dart Pad | dart online ground

### Basics
- print 
- 未初始化的变量的初始值为null
- 1.12 => null-aware(?.  ??)
- fn和js的差异主要在声明
- Future ｜ Promise（JS）


## Flutter
### Basic
- 命令式imperative｜声明式declarative UI（不管是原生还是Web，都经历了这样的过程）
- 视图配置（like Widget）
- create|run|import
- import => material.dart(Material Design) | Cupertino(IOS风格Widget) | widgets.dart(基本窗口集)

### 资源
- Android - resources
- IOS - Images
- flutter - Assets引用方法 - pubspec.yaml中声明
- device Pixel Ratio
```
ldpi 0.75x | mdpi 1.0x | hdpi 1.5x | xhdpi 2.0x | xxhdpi 3.0x | xxxhdpi 4.0x
```
- images/xxx.png  | images/2.0x/xxx.png
- IOS - Localizable.strings | Flutter - flutter_localization && intl && easy_localization

### 依赖
- Android - Gradle
- IOS - Podfile
- 仅在添加单平台相关的文件时候使用Podfile和Gradle文件
- pub.dev
- dart构建系统｜pub管理依赖

### View 视图
- Android - View
- IOS - UIView
- Widget

### 布局
- Android - XML
- IOS - Storybook ｜ view controller
## modules

### Scaffold

### PageView

### Navigator

### List

### Image


### NotificationListener
### 自定义组件
### Native Modules
### AI Voice

## Network && Storage
### http

## Channel


## Plugins
### Flutter
### Native
### 自定义



# Part2 - 领域工程化，环境相关

## ENV（具体Tips可参考之前“Flutter 开发环境配置”的博文）
- 官方文档配置即可
- 用好flutter doctor命令帮忙解决问题
- 镜像按需配置（科学上网之后可忽略 
- bash or zsh 配置（PATH ｜ storage_base_url && hosted_url）
- ```PUB_HOSTED_URL https://pub.flutter-io.cn | FLUTTER_STORAGE_BASE_URL https://storage.flutter-io.cn```
- Andriod Studio 也可进行环境变量配置 - 按需
- Xcode - 安装&&命令行工具配置&&许可协议
- IOS模拟器（Window > Scale）
- 热加载-r｜热重启-R
- Android Studio（按官方文档操作就行） - 机器上设置好硬件加速（VM acceleration）
- Android Studio安装Flutter和Dart插件（perferences 选 plugins，搜对应关键词）
- Android Studio - Andriod SDK 下载对应的（preferences 搜 Android SDK），View - VSC里面可视化版本控制
- emulator -avd xxx (bash or zsh里面可配置好 emulator 路径)

## 真机
### IOS 
- homebrew - 安装相关库
- worksapce - 进行设置（bundle id 确保唯一 - 不然自动签名会失败）
### Andriod
- 设备上启用开发人员选项和USB调试
- ```flutter devices```

## IDE
### VS code
- Andriod无法直接调试
### Android Studio

## Hybrid


## Update && Upgrade



## Build && deploy

# Part3 - 业务模块
### 