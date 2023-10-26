---
title: 松本行弘的程序世界-我为什么开发Ruby-面向对象-程序块-设计模式-Ajax-RoRs-阅读笔记
date: 2021-11-29 14:46:23
tags:
---
## 我为什么开发Ruby
> 因为它给我带来了快乐
> 松本行弘. 松本行弘的程序世界 (图灵程序设计丛书) (Chinese Edition) (Kindle位置116). 人民邮电出版社. Kindle 版本. 

### Lines
- 语言体现了人类思考的本质
- 程序员由于使用的编程语言不同，他的思考方法和编写出来的代码都会受到编程语言的很大影响。
- Ruby编程语言的设计目标是，让作为语言设计者的我能够轻松编程，进而提高开发效率。
#### 设计原则
- 简洁性
 - Lisp(Paul Graham - 简洁就是力量)
 - Ruby不进行明确的数据类型定义，不必要的声明都可以省略
 - 如果可以把伪码中非实质的东西去掉，只保留描述算法的部分就直接运行，那么这种编程语言不就是最好的吗？Ruby的目标就是成为开发效率高、“能直接运行的伪码式编程语言”
- 扩展性
 - 实现扩展性的一个重要方法是抽象化
 - 很多面向对象或者函数式的现代编程语言，都在抽象化方面做得很好
 - 关于扩展性，有一点是不能忽视的，即“不要因为想当然而加入无谓的限制”。比如说，刚开始开发Unicode时，开发者想当然地认为16位（65535个字符）就足够容纳世界上所有的文字了；同样，Y2K问题也是因为想当然地认为用2位数表示日期就够了才导致的。从某种角度说，编程的历史就是因为想当然而失败的历史。而Ruby对整数范围不做任何限定，尽最大努力排除“想当然”。
- 稳定性
 - 拒绝了宏
 - 稳定的语法

## 面向对象
### 编程和面向对象的关系
### 数据抽象和继承
### 多重继承的缺点
### 两个误解
### duck Typing诞生之前
### 元编程


## 程序块
### 程序块的威力
### 用块做循环
### 精通集合的使用


## 设计模式



## Ajax
- https://developer.mozilla.org/zh-CN/docs/Web/Guide/AJAX
- https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest
- 90年代末 - MS Outlook =>IE (XMLHttp) | 其他浏览器XMLHttpRequest => 使浏览器能从JavaScript中发出Http请求
- 2005 => Jesse James Garrentt => https://courses.cs.washington.edu/courses/cse490h/07sp/readings/ajax_adaptive_path.pdf => 本质：用XHR获取数据，然后修改当前页面
- 创建XHR对象 - 告诉该对象要请求什么信息，设置成功或错误处理程序，然后实际地发送请求（new | open | onload | onerror | send）
#### fetch - 新的API
- 基于promise
- https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API

## Ruby on Rails
### MVC 和 Ruby on Rails
### 开放类和猴子补丁

###
etching bundler-2.3.26.gem
ERROR: While executing gem ... (Gem::FilePermissionError)
You don't have write permissions for the /Library/Ruby/Gems/2.6.0 directory.
这个错误意味着你没有足够的权限来向这个目录写入文件。这在OS X上是常见的问题，因为这个目录是由系统拥有的。

要解决这个问题，你有两个选择。

第一个选择是使用sudo命令来运行gem install：

```bash
sudo gem install bundler -v 2.3.26
```

这将给你足够的权限来安装gem，但是这可能会让你的系统环境被修改，这是一种不推荐的做法。

第二个更好的选择是安装一个版本管理器，例如RVM或RBENV。这些版本管理器为你的Ruby版本和Gem创建了一个单独的环境，这样你就可以在不修改系统环境的情况下安装它们。

例如，你可以通过下面的步骤安装RVM和新版本的Ruby：

```bash
\curl -sSL https://get.rvm.io | bash -s stable
rvm install 2.7.0
rvm use 2.7.0
gem install bundler -v 2.3.26
```

这将安装RVM，然后使用RVM安装Ruby 2.7.0，然后切换到这个新版本的Ruby，最后安装所需版本的bundler。