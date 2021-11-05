---
title: css应用总结
date: 2021-10-09 18:35:06
tags:
---
### 分页
> 做的PDF打印的服务

#### break
- 用于模版的分页处理
- block元素（不脱离文档流，非弹性布局）
- page-break-after | page-break-before | page-break-inside
- https://developer.mozilla.org/zh-CN/docs/Web/CSS/page-break-after
- break-after
- https://developer.mozilla.org/zh-CN/docs/Web/CSS/break-after
- inside用avoid，避免元素被分割，例如本项目中题目index|tag|icon等元素
- after用always，在需要插入分页的地方使用

#### orphans | windows


