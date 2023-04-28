---
title: cocos-creator-summary
date: 2022-11-19 16:02:11
tags:
---
## 文档&论坛
- http://docs.cocos.com/creator/manual/zh/getting-started/install/
- https://forum.cocos.org/

## 设置 - language - 可以切换语言


## basic 
- Cocos Creator 是一款基于 Cocos2d-x 引擎的游戏开发工具，它实现了组件式开发、场景编辑器、动画编辑器等丰富特性
- Cocos Creator 3.x 是该引擎的最新版本，相较 2.x 的版本，它在渲染、物理、脚本系统等方面有很大的改进

1. 基础架构

Cocos Creator 使用的是基于 Entity-Component-System (ECS) 的组件化开发模式。
在 ECS 架构中
实体 (Entity) 是游戏世界中的各个独立对象，如游戏角色、场景物体等；
组件 (Component) 是用来描述实体的属性和行为的模块，如渲染、物理、用户输入等；
系统 (System) 是用来处理组件之间的交互和更新组件状态的逻辑。

Cocos Creator 中的实体使用 `Node` 类来表示，组件使用 `Component` 类，系统使用 `System` 类。开发者可以通过创建自定义组件和系统来拓展游戏的功能。

2. 渲染

Cocos Creator 3.x 的渲染系统使用了全新的渲染管线，支持高性能的 native 渲染和 Web 渲染。核心渲染相关的代码位于 `engine/renderer` 目录下。

主要的渲染类有：

- `Pipeline`：渲染管线，负责渲染任务的调度处理。
- `RenderView`：渲染视图，用来定义各种渲染参数。
- `Pass`：渲染过程，描述了绘制一次材质的操作。
- `FrameBuffer`：帧缓冲区，用于存储渲染生成的像素数据。

Cocos Creator 支持 forward 渲染管线（正向渲染）和 deferred 渲染管线（延迟渲染），可以根据游戏需求选择合适的渲染方式。

3. 物理

Cocos Creator 3.x 集成了开源物理库 Ammo.js 和 cannon.js，为开发者提供了一整套的物理系统解决方案。核心物理相关的代码位于 `engine/physics` 目录下。

主要的物理类有：

- `RigidBody`：刚体，用于表示物体的质量、速度等属性。
- `Collider`：碰撞器，用于检测物体之间的碰撞。
- `PhysicsSystem`：物理系统，用于处理刚体、碰撞器的更新和物理世界的模拟。

4. 脚本系统

Cocos Creator 3.x 支持 JavaScript 和 TypeScript 两种脚本语言，开发者可以选择自己熟悉的语言进行游戏开发。核心脚本相关的代码位于 `engine/scripting` 目录下。

主要的脚本类有：

- `Script`：脚本基类，所有的游戏脚本都需要继承自这个类。
- `Component`：组件脚本基类，用于创建自定义组件。
- `System`：系统脚本基类，用于创建自定义系统。

#### gfx
gfx（Graphics API Framework，图形 API 框架）是 Cocos Creator 3.x 引擎的图形渲染部分的底层实现。它是一个跨平台的图形 API 抽象层，可为不同的图形 API 提供统一的接口。引擎通过 gfx 来实现跨平台渲染的能力。这个框架使得引擎可以在不同的平台上适配不同的底层图形 API，例如 WebGL、WebGL2、Metal、Vulkan 和 Direct3D 等。

gfx 主要包括以下几个部分：

抽象层：这里定义了所有跨平台的图形 API 的基本接口，例如管线、缓冲区、纹理、着色器等。开发者可以使用这些接口编写能在不同平台上运行的渲染代码。

API 实现层：这个层次实现了 gfx 抽象层中各个接口的具体实现。针对每种图形 API，引擎都实现了一套 API 实现层。这里包括 WebGL、WebGL2、Metal、Vulkan 等对应的 API 实现。

命令缓冲：为了优化渲染性能，引擎采用了命令缓冲的技术，将渲染命令先缓存起来，然后在合适的时机统一提交给 GPU。这样可以减少 CPU 和 GPU 之间的通信成本，提高渲染性能。

资源管理：gfx 还提供了一套资源管理机制，让开发者可以方便地管理渲染所需的资源，如纹理、缓冲区、渲染目标等。这一部分也会处理资源生命周期和内存管理等问题。

通过 gfx，Cocos Creator 3.x 在底层实现了一套高效、跨平台的渲染系统。从而使开发者可以专注于游戏逻辑的开发，而无需关心不同平台的底层实现细节。


### 发布

#### 小程序
- https://developers.weixin.qq.com/minigame/dev/guide/game-engine/cocos-laya-egret.html
- 物理静音键问题

### web audio
- https://mp.weixin.qq.com/s/8DCFok78lzqgCrp_w5rEmw