---
title: v3-overall-design
date: 2022-02-18 20:11:38
tags:
---
## trade-on
> 框架设计层面
- 范式 => 命令式-关注过程 ｜ 声明式-关注结果
- 性能 -（理论上 - 命令式 > 声明式） ｜ 可维护性 == 心智负担
- 运行时 - Render｜ 编译时 - Complier - svelte ｜ 运行时-编译时 - vue （v3通过编译手段提升性能）
- 虚拟DOM - 让diff的性能消耗最小化
- comparison - document.createEl | virtual Dom | innerHTML => 页面大小｜变更部分大小｜create？update？