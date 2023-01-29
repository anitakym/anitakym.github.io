---
title: egret-and-游戏设计
date: 2022-01-04 10:03:09
tags:
---
> 少儿的学习小游戏，内容团队之前基于白鹭引擎和自研的课件编辑平台进行创作；内容具体设计，制作者按学科划分，每个学科有具体的一套从设计到实现的人员链; 

## Basics
### 官方说明
```
白鹭科技专注技术创新，攻克底层技术制约，为开发者带来一整套游戏研发解决方案，自主研发了白鹭引擎（Egret Engine）、Egret Pro、白鹭加速器（Egret Runtime）、骨骼动画工具(Dragon Bones)、可视化编辑器（EUI Editor）等多款产品，让开发者简单、高效的开发出移动游戏。
- https://www.egret.com/about
- Egret Engine 是一款使用 TypeScript 编写的 HTML5 游戏引擎，包含渲染、声音、用户交互、资源管理等诸多功能，解决了 HTML5 性能、碎片化问题，应用于 2D 游戏、3D 游戏开发，及移动端交互式应用构建，拥有完善的跨平台运行能力。 现在 Egret Engine 及其它工具已全部整合到 Egret Launcher，请大家直接下载安装开启您的游戏项目创作。
```


### 教学游戏
- http://gk.link/a/1195n





## others
### oasis
- https://github.com/oasis-engine/engine
### 2048
- 游戏：逻辑，技术，架构，创意，美术
- UI（V） 动画效果逻辑 游戏主逻辑（C） 支撑逻辑 游戏数据（M）
- 1.加载各项资源（board（Array）， score） 
```
grid-container position：relative grid-cell position:absolute
在main.js里面：
 $().ready(){} ——加载 
function newgame() { 
  //初始化棋盘格 init()——两个for循环，创建grid-cell-x-y 
  .css()控制位置,具体的实现可以调用support.js里面的函数。 //在随机两个格子生成数字 number-cell —— var board 遍历数组 updateBoardView（）
  number-cell是动态定位，pos:absolute
  数字的生成也可以带一点动画，这个可以将方法写在动画的控制逻辑
}
```
- 2.游戏循环 基于时间的游戏循环 基于玩家响应的循环（JS事件响应机制）
- 3.交互细节 canMoveLeft() 左边是否没有数字 左边数字是否和自己相等 遍历
- 交互逻辑调试

#### webAssembly在白鹭引擎中的实践
- 需要提高JS运行效率
- https://zhuanlan.zhihu.com/p/30513129