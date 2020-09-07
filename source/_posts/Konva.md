---
title: Konva
date: 2019-11-19 17:09:57
tags:
    - 图形图像
    - 工作经验总结系列
---
> 作业批改（教学），海报生成（运营）是两个主要使用场景，需要借助canvas；Konva是目前采用的一个库

### canvas
The HTML <canvas> element provides an empty graphic zone on which specific JavaScript APIs can draw (such as Canvas 2D or WebGL).

The default size of the canvas is 300 px × 150 px (width × height).

官方文档指路：https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/canvas


### canvas tips
- 页面像素大于阈值（根据不同端的不同设备不一样）的情况下，canvas是不能绘画出来的。
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <canvas id="canvas" width="16385" height="16380"></canvas>
    <script>
        const canvas = document.getElementById('canvas');
const ctx = canvas.getContext('2d');

ctx.fillStyle = 'green';
ctx.fillRect(10, 10, 150, 100);

    </script>
</body>

</html>
```
如上，就是Chrome("Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.125 Safari/537.36")浏览器,当超过这个阈值后，绘画当方框无法显示出来。

- 走势图高级绘图板的开发（画线图形算法，橡皮擦（兼容全系浏览器））—— 数据多的时候，保持性能。
