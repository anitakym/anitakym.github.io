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
- View和Controller容易膨胀
- View和Model没有完全分离
#### MVP
- View和Model完全分离，可以修改试图而不影响模型，交互都发生在Presenter
- Presenter与View的交互是通过接口来进行的，方便单元测试
- 页面逻辑复杂的话，响应的接口也会变多，增加维护成本
#### MVVM
- ViewModel只负责处理和提供数据
- ViewModel里面只包含数据和业务逻辑，没有UI，方便单元测试
- 数据绑定使得程序较难调试，因为数据都是自动更新到UI

#### AOP
- OOP
```
类：代码以函数（Method）和字段（Field）的形式封装在类中
函数：定义函数签名和函数体
函数题：定义函数的执行逻辑
编译器：将源代码转换成可执行代码
```
- AOP 
```
类：代码以切点（PointCuts），属性（Attributes）、植入（Advice）的形式封装在类中
切点：定义植入（Advice）的锚点
植入：定义需要植入的逻辑
植入器：将植入逻辑插入到锚点处
```

#### loC
- 直接依赖：一个对象A要完成其功能，通常需要依赖于其他对象B，C等，其具体的实现方式就是在对象A中构建（new）其所依赖的对象B、C等，这就相当于A控制了它所依赖的对象B、C
- 控制反转：打破A直接控制B这层关系，B对象的生命周期交由loC容器来控制，A不用再去寻找和初始化（控制）其所依赖的B、C了，只用等着loC容器的投喂就可以
- 实例SPI

### 大的架构手段
- 单体架构
- 分离架构
- 分层架构
- 服务化架构
  - 需要约定模块可以对外提供的能力
  - 模块之间需要遵循相同的调用方式
  - 旧的模块需要按照相同的标准来改造
  - 使用方不应该直接依赖于实现方
- 事件驱动架构
- 宿主-插件架构
- 微内核架构
- 微服务架构
- 领域驱动架构

## summary
- 不同架构手段对共同目标是高内聚低耦合
- 找到适合业务场景的脚骨
- 一个复杂系统是多种架构模型的组合体

定义问题 确定架构 方案落地 结果复盘