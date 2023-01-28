---
title: netty-summary
date: 2023-01-20 11:20:07
tags:
---



## study
- https://github.com/arthur-zhang/netty-study.git

### source code
- backlog
- ServerBootstrapAcceptor
- io.netty.channel.nio.AbstractNioChannel#AbstractNioChannel 
- io.netty.channel.nio.AbstractNioChannel#doBeginRead
- io.netty.channel.nio.NioEventLoop#run
- Reactor 模型
- 事件循环模式
- Allocator
- 边缘触发
- 水平触发
- io.netty.channel.AbstractChannelHandlerContext#write(java.lang.Object, io.netty.channel.ChannelPromise)
- Netty Idle检测
- NioEventLoopGroup
- 零拷贝
- ByteBuf
- ByteBuf 的读写操作是非阻塞
- Netty Recycler
- FastThreadLocal