---
title: css-tricks-summary
date: 2022-09-06 14:02:46
tags:
---

## 一些基本的总结
#### event偏移量
- 相对左上角
screen - 屏幕 | page - 网页区域 | client - 浏览器可视区域 | offset - 父节点区域（无则是`<html>or<body>`）

#### 问题分类
- 结构 | 背景 | 点击 | 切换 | 悬浮 | 表单


## 变量
- 基于变量与JS通信，简化基于JS逻辑的效果
#### 放大镜
- scss
- 变量（offset偏移量）随着鼠标移动而改变，offset控制伪元素的绝对定位
- 伪元素的background实现放大镜显示内容
- https://codepen.io/JowayYoung/pen/oNbGzPy

#### 滚动渐变背景
- event.target.scrollTop
- 把鼠标相关参数赋值到变量中

## 光影斑驳效果
https://css-tricks.com/css-dappled-light-effect/






## tools
- https://codepen.io/
- https://caniuse.com/
- https://csstriggers.com/
- https://cubic-bezier.com/
- https://xluos.github.io/demo/flexbox/
- https://gs.statcounter.com/
- https://github.com/JowayYoung/idea-css