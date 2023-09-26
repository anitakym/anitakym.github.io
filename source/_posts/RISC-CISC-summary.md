---
title: RISC-CISC-summary
date: 2023-09-25 10:17:39
tags:
---

ARM 和 x86 是两种主流的 CPU 架构，各自遵循不同的设计理念。

1. ARM (Advanced RISC Machine): ARM 架构遵循 RISC (Reduced Instruction Set Computing, 精简指令集) 设计原则。RISC 系统的一部分特性包括每个指令的执行时间都相当短（通常是一个时钟周期）以及指令的数量较少。这通常导致更高的处理器效率、更低的电力消耗，非常适合于手机、平板电脑等移动设备。

2. x86: x86 架构遵循 CISC (Complex Instruction Set Computing, 复杂指令集) 设计原则。CISC 指令集的一部分特性包括每条指令可以执行多个低级操作，如加载、存储、运算等。得益于这样的设计，x86 架构通常有着更强大的性能和灵活性，非常适合于服务器、桌面计算机等高性能计算平台。

当然，现代 ARM 和 x86 架构已经大幅融合了彼此的优点，比如x86 在功耗优化、ARM 在性能提升方面都做了许多努力。因此，这两者的界限已经开始模糊。

苹果在2020年开始将其Mac设备从使用Intel的x86架构处理器转换为自家设计的基于ARM架构的Apple Silicon处理器。这些基于ARM的Apple Silicon被称为M1芯片。以下是截至目前使用Apple Silicon M1的Mac设备：

1. MacBook Air (2020年末版及其后的版本)
2. 13英寸MacBook Pro (2020年末版及其后的版本)
3. Mac mini (2020年末版及其后的版本)
4. 24英寸iMac (2021年中及其后的版本)
5. MacBook Pro (2021年，带有14英寸和16英寸的M1 Pro或M1 Max芯片)

未来，预计苹果会继续扩大其基于ARM的Mac产品线，取代现有的Intel x86架构Mac。

### electron - arm dmg