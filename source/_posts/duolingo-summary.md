---
title: duolingo-summary
date: 2024-02-28 16:27:33
tags:
---
- wasm
- Service Worker
```
sw
 gcm.js
 offline.js
gcm-service-worker.js
```
OffscreenCanvas 是一个 HTML5 Canvas API，允许你在Web Worker中创建和操作 Canvas 2D 或 WebGL 上下文。Web Worker 是一种能在浏览器的背景线程中运行脚本的方法，这样就不会阻塞用户界面。

OffscreenCanvas 的主要优势在于，你可以在后台线程中进行复杂的渲染计算工作，然后渲染结果可以直接传输给前台的画布进行显示，这样不会影响到前台主线程的性能。

以下是创建一个 OffscreenCanvas 的例子：

```javascript
const offscreenCanvas = new OffscreenCanvas(256, 256);
const context = offscreenCanvas.getContext('2d');
// 在这里，你可以使用 getContext() 方法中的 '2d' 或 'webgl' 参数，根据你的需要来获取相应的 2D 或 WebGL 渲染上下文。
```

然后可以在这个上下文上利用各种方法进行绘图操作。


### 163邮箱中使用的service worker
- workbox(https://github.com/GoogleChrome/workbox)