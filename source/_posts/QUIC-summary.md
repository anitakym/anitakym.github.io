---
title: QUIC-summary
date: 2024-03-12 11:09:18
tags:
---
QUIC（Quick UDP Internet Connections）是由Google开发的一种基于UDP的传输层协议，目的是菜单网络连接更为快速、安全。QUIC 在设计时借鉴了TCP、TLS (Transport Layer Security) 和 HTTP/2 的一些特性，但并不是这三者的简单组合。

关于QUIC，有一些特点是需要了解的：

1. **快速连接建立**：传统的基于TCP的协议在建立连接时需要进行三次握手，如果加上TLS加密，那就需要2-3个RTT（Round-Trip Time，往返时延）。而QUIC协议只需要一个 RTT即可完成握手过程，如果是之前已经“见过”（即在缓存中有记录）的服务器，甚至可以做到零RTT。

2. **内建 TLS**：QUIC协议的连接建立过程中，也完成了TLS握手过程，因此在传输数据时，已经实现了加密。

3. **流控制”，拥塞控制和丢包恢复**：QUIC内置了一系列优化，并且加入了基于流的窗口以及并发多流的拥塞控制。

4. **连接迁移**：由于传输层的连接上下文保存在客户端，所以当网络环境发生变化时，可以实现无缝的连接迁移。

5. **多路复用**：允许在一个QUIC连接中同时存在多个stream，实现数据的并行传输。

QUIC协议正在逐渐被采用，特别是在现代Web传输协议 HTTP/3中，QUIC被选为默认的底层传输协议。

- https://github.com/Tencent/tquic/tree/develop
- https://tquic.net/zh/docs/tutorial/core_concepts/

### 比较
- https://tquic.net/zh/docs/further_readings/comparison