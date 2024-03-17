---
title: 基于sharp提供图片处理服务
date: 2023-08-30 11:24:41
tags:
---
- https://sharp.pixelplumbing.com/
- https://github.com/lovell/sharp


`sharp` 是一个用于处理图片的高性能 Node.js 模块，大量使用了本地资源，并且选用的内存分配策略在某些系统或架构上可能会引发问题。

当你使用类似 `sharp` 这种包时可能会出现内存申请错误，部分原因可能是 Node.js 默认的内存分配器 `ptmalloc` (或在某些版本中的 `tcmalloc`) 与 `sharp`引用的本地库的内存管理发生冲突。

解决这种问题的一个办法就是更换 Node.js 的内存分配器。你可以试试使用 `jemalloc` 或者 `tcmalloc`。这些分配器可以清晰地分隔 Node.js 堆外的内存，规避 `ptmalloc` 可能存在的问题。

要使用 `jemalloc`，你需要在系统中安装它（在 Ubuntu 上可以使用 `sudo apt-get install libjemalloc-dev`），然后在启动 Node.js 时设置环境变量 `LD_PRELOAD`。具体做法是在启动脚本前加一个环境变量声明，比如 `LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libjemalloc.so node app.js`。

另外，为确保 `sharp` 正常工作，也请确保你的系统上已安装了其需要的依赖项，如 `libvips` 库。在 Docker 环境中，考虑选择 ubuntu 或 debian 打底的镜像基础，避开 Alpine。因为 `sharp` 的一些依赖在 Alpine 中可能会有问题。

最后，对于大型项目或在生产环境中，最好是进行充分的内存管理测试，以确保选用的方案能在所有预期的使用情况下正常工作。