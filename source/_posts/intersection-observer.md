<!--
 * @Author: yimin kuang
 * @Date: 2024-07-25 18:03:35
 * @LastEditors: yimin kuang
 * @LastEditTime: 2024-07-26 14:43:30
 * @Description: 描述信息
-->
---
title: intersection-observer
date: 2024-07-25 18:03:35
tags:
---
https://caniuse.com/?search=intersection
https://developer.mozilla.org/zh-CN/docs/Web/API/IntersectionObserver

IntersectionObserver 是一个浏览器的 API，它提供了一种异步观察目标元素与其祖先或视窗(viewport)交叉状态的方法。这个 API 是为了解决“你需要知道一个元素是否在视窗中可见”这类问题而设计的。

这个 API 的主要用途包括：
1. 懒加载：当元素进入视窗时，开始加载内容。
2. 无限滚动：当你滚动到页面底部时，自动加载更多内容。
3. 报告广告的可见性：只有当广告在视窗中可见时，才报告广告的展示次数。

使用 IntersectionObserver 的基本步骤如下：
1. 创建一个 IntersectionObserver 实例，传入一个回调函数和选项对象。
2. 使用 observer.observe(target) 方法来开始观察一个目标元素。
3. 当目标元素的交叉状态发生变化时，回调函数会被调用。回调函数会接收到一个 IntersectionObserverEntry 对象的数组，每个对象都代表了一个目标元素的交叉状态信息。
4. 当你不再需要观察一个元素时，可以调用 observer.unobserve(target) 方法。当你不再需要观察任何元素时，可以调用 observer.disconnect() 方法。

