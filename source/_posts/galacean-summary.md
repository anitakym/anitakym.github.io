---
title: galacean-summary
date: 2023-11-06 16:36:18
tags:
---
https://galacean.antgroup.com/#/examples/latest/lottie-benchmark

骨骼动画（Skeletal Animation）以较小的内存占用来生成抽象和复杂的动画。它通过对“骨骼”进行动画设计，然后使用这些骨骼来驱动模型的不同部分，创建出逼真的动画。

在骨骼动画中，减少骨骼数量能够降低硬件计算压力，从而提高性能，特别是在某些硬件配置较低的设备中。

苹果的 iPhone 设备有一个知名的限制是，它的 GPU 对 uniform 的数量有一定的限制。如果一个动画的骨骼数量超过这个限制，将不能正确地在这些设备上运行。因此，开发者在制作动画时需要考虑这些限制，并适应性地进行优化。

 JavaScript 不擅长于进行密集计算，但现在有很多工具和框架来处理这方面的问题。例如，WebGL 和 WebAssembly 可以使得在浏览器中执行高性能的数学和图形计算成为可能。

 ```
 苹果的 iPhone 和一些其他设备存在一些 GPU 限制，其中之一就是对 uniform 的数量有一定限制。

Uniforms 是一种 WebGL（一种在浏览器中使用 GPU 的方式）中的概念，它们是从 JavaScript 发送到顶点着色器或片段着色器的数据。一般来说，它们用于存储时间、灯光、纹理样本器等值。

苹果设备上的这个限制通常表现为最大工作负载（最多可以多少个 uniforms）。这个数量取决于设备的 GPU。对于某些早期或者入门级别的设备，这个限制可以低至 128 个 uniforms。

这个限制在实际开发中可能会成为问题，特别是在开发复杂的 WebGL 应用，如 3D 游戏或者复杂的数据可视化应用时。达到 uniform 的限制可以导致应用无法正常渲染，甚至出现崩溃。

解决这个问题的一种常见方式是更好地管理和优化你的 uniforms。比如，尽量减少不必要的 uniforms，复用 uniforms，或者使用纹理来存储数据以降低对 uniforms 的需要。

需要注意的是，这个问题并不只存在于 iPhone 上，一些旧的或低端的 Android 设备上也可能存在相同的问题。同样，在 WebGL 2 中，这个限制已经得到了一定的提高，但是考虑到设备兼容性，开发者仍然需要注意这个问题。
 ```


 ### galacean effect
 https://galacean.antgroup.com/effects/inspiration



 ### 其他
 - https://github.com/svga/SVGAPlayer-Web-Lite