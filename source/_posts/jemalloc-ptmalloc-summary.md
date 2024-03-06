---
title: jemalloc-ptmalloc-summary
date: 2024-03-06 11:24:20
tags:
---

- https://internals.rust-lang.org/t/jemalloc-was-just-removed-from-the-standard-library/8759
rust 从默认的jemalloc,该回了系统malloc

`jemalloc` 是一种开源内存分配库，有时由于其提供的优化性能，开发者会希望使用它替代默认的 `ptmalloc`，下面是在 Linux 上做此类替换的一般步骤：

1. 首先，我们需要安装 `jemalloc`。在 Ubuntu 上，可以使用 `apt-get`：
```
sudo apt-get install libjemalloc-dev
```

2. 创建一个包装脚本以将 `jemalloc` 插入到库加载序列的最前面。这实际上会将 `LD_PRELOAD` 环境变量设置为 `jemalloc` 的路径，以此在应用启动时优先加载 `jemalloc`。
```bash
#!/bin/bash
export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libjemalloc.so.1
exec "$@"
```
假设该脚本命名为 `use_jemalloc.sh`。要打开文件并使其可执行，我们可以运行：
```bash
chmod +x use_jemalloc.sh
```

3. 现在我们可以使用此脚本启动我们的应用，例如：
```bash
./use_jemalloc.sh node app.js
```

上述步骤将确保你的 Node.js 应用使用 `jemalloc` 而不是默认的 `ptmalloc`。

提示：`jemalloc` 的路径可能因操作系统和版本不同而异。如果 `/usr/lib/x86_64-linux-gnu/libjemalloc.so.1` 不起作用，你可能需要在你的系统中搜索正确的路径。

不过，即便执行了上述步骤，也不能保证一定能提升性能，这很大程度上取决于你的特定应用和工作负载。这是一个值得试验的方面。如果你没有看到预期的性能改进，你可能需要更深入地研究或者考虑其他的优化方法。


Node.js 应用 RSS 内存泄漏排查与解决方案
https://zhuanlan.zhihu.com/p/675317993
```
故事从一次 Node.js 20 升级开始
一直走弯路，Node.js 16、18 就存在此问题
第一次的 RSS 内存分析结论：内存碎片比较多没有及时回收
问题结果：周期性 OOM
故事再次循环
复现代码
TestCase1
TestCase2
npmmirror 使用 jemalloc 的修复效果
通过 ezm 摸排有多少类似的应用
只有 Node.js 出现此类问题吗？
为什么 2009 年 Facebook 就提供 jemalloc 解决此问题而 Node.js 在 2023 年还在发生？
相关资料
故事从一次 Node.js 20 升级开始

```