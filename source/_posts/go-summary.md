---
title: go-summary
date: 2022-10-20 20:54:01
tags:
---
## go
#### what
- 高性能，高并发
- 语法简单，学习曲线平缓
- 丰富的标准库
- 完善的工具链
- 静态链接
- 快速编译
- 跨平台
- 垃圾回收

#### 应用-公司
- 字节，腾讯，美团，滴滴，百度，谷歌。Facebook。七牛云，bili, pingcap

#### 字节why - go
- 最初python，性能问题换成了go
- C++不适合在线Web业务
- 早期团队非Java背景
- 部署简单，学习成本低
- 内部RPC和HTTP框架的推广
#### 开发环境
- golang安装
- 配置集成开发环境
- 基于云的开发环境 

#### 语言基础语法

## 进阶
- 并发编程
### 并发VS并行
> go可以充分发挥多核优势，高效运行
#### Coroutine
- 用户态-内核态
- 线程：用户态，轻量级线程，栈MB级别
- 协程：内核态，线程跑多个协程，栈KB级别

#### CSP - communicating sequential processes
- 通过通信共享内存
- 通过共享内存实现通信
- 提倡通过“通信共享内存”而不是通过共享内存而实现通信

#### channel
- make（chan元素类型，[缓冲大小]）
- 无缓冲通道 - make(chan int)
- 有缓冲通道 - make(chan int,2)

#### 并发安全lock

#### WaitGroup

## 依赖管理
- 背景：工程项目不可能基于标准库0～1编码搭建
- 管理依赖库
#### go依赖管理演进
- 不同环境（项目）依赖的版本不同
- 控制依赖库的版本
- GOPATH | Go Vendor | Go Module

#### GOPATH
- 场景：A和B依赖于某一package的不同版本
- 问题：无法实现package的多版本控制

#### Go Vendor
- 项目目录下增加vendor文件，所有依赖包副本形式放在$ProjectRoot/vendor
- 依赖寻址方式： vendor=>gopath
- 通过每个项目引入一份依赖的副本，解决了多个项目需要同一个package依赖冲突问题
- 无法控制依赖的版本
- 更新项目又可能出现依赖冲突，导致编译出错



