---
title: vscode插件使用合集
date: 2020-08-06 15:37:05
tags:
    - 工具篇
---

#### vscode
常用快捷键：
- 显示所有命令（cmd + shift + P）
- 转到文件（cmd + P）
- 在文件中查找（cmd + shift + F）
- 开始调试（F5）

#### vscode-faker
使用方法
```
export default `
Abbott
Turner
Kutch
Reichert
Funk
Mante
Hammes
Howell
`.trim().split(/\s+/g)
```
生成一个name的数组

> 怎么生成一行一个名字呢？
<strong>vscode-faker</strong>

1. 利用多行选择和faker
2. alt+shift (先点击第一行，按完快捷键后，再点击最后一行)
3. 再cmd+shift+p调出faker，选中要生成的类型即可

#### open in browser

我的chrome浏览器之前一直没有反应，升级了之后就好了（但是也是只在没有打开过浏览器页面的情况下生效

那么open in browser or view in browser 的原理是什么呢

插件评级星星边上有repository，可以通过这个点到github里面去看他们具体的实现


