---
title: Android-design-notes
date: 2023-01-11 17:39:00
tags:
---

手段
业务抽象
分而治之
标准规范
组织管理

演进
解决问题
保持重构
迭代升级
应对衰退

公共问题
- 编程思想
- 问题分解
- 领域建模
- 服务治理
- 流程机制
- 架构标准

业务发展 - 越来越复杂 - 必然趋势
- 理解成本变高
  - 宏大的规模不好理解
  - 复杂的结构不好理解

- 预测难度变大
  - 业务变化
  - 技术变化

## Android OS
#### 应用框架层
App开发者直接使用的接口层，UI的实现，数据的处理，资源的使用，都是用这一层的API
#### Binder IPC
提供跨进程访问的能力，App可以高效的访问由系统进程暴露的能力，App进程与系统进程之间的通信是典型的C/S模型
#### 系统服务
提供窗口管理，相机，音视频等系统能力，包含各种子系统，内部逻辑很庞大，往下调用HAL层封装的硬件能力；往上通过Binder暴露可以远程调用的API

#### 硬件抽象层
屏蔽底层不同驱动的差异，使得系统服务层可以快速适配到不同的硬件设备

#### Linux内核
CPU、内存、唤醒服务等重要的驱动实现都给予该层操作系统等核心实现

## IOS
#### 应用框架层 Cocoa touch(application layer)
- EventKit
- GameKit
- MapKit
- PushKit

#### 图形图像层 media layer
- ULKit
- Animation
- Graphics
- Images

#### 核心服务层 core services
- Location
- Motion
- Health
- GPS
- Telephony
- Foundation

#### 内核层 core os
- Bluetooth
- Security
- Accessories

### Android vs IOS
Activity  ViewController
Intents   Segues/ViewControllers
Service   "Backgrond Mode"
ContentProvider   CoreData
Layouts   Storyboards and scenes

## Flutter
#### UI框架层
提供不同样式的组件和动画，声明式UI，Dart作为编程语言，同时支持JIT和AOT
#### 引擎层
将上层定义的UI树转换成屏幕像素，提供平台调用接口和Dart虚拟机

#### 嵌入层
Flutter引擎需嵌入不同的平台

- 架构设计是为了解决特定领域不同发展阶段的业务问题
- 不同领域的架构有明显的技术差异，但是也有相似性
- 架构要面临技术挑战，还要应对组织业务膨胀的熵增
- 移动端需要利用有限的设备资源设计符合小屏幕的架构


### 小的架构手段
#### GoF设计模式
#### MVC
#### MVP