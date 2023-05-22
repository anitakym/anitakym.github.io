---
title: UUID-summary
date: 2023-05-22 16:35:13
tags:
---
### UUID


#### nanoid
与UUID的比较
Nano ID与UUID v4（基于随机）相当。它的ID有类似的随机位数（Nano ID为126，UUID为122），所以它有类似的碰撞概率：

要想有十亿分之一的重复机会，必须产生103万亿个版本4的ID。

Nano ID和UUID v4之间有两个主要区别：

Nano ID使用更大的字母表，所以类似数量的随机比特被包装在仅仅21个符号中，而不是36个。
Nano ID代码比uuid/v4包小4倍：130字节而不是423字节。