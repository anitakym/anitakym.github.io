---
title: IM-basic
date: 2024-10-12 13:52:33
tags:
---
### IM聊天场景
以人为中心的通信系统。消息转发的可靠性、吞吐量、及时性是业务上的一个难点。

### Live直播场景
以群为中心的通信系统，通常称作聊天室。在一个聊天室中，你需要在设计时考虑到一个房间可能有10w+的在线用户，不过在聊天室场景中用户不可能同时在多个room中，因此可以通过路由把相同room的用户切到同一台服务，达到最大化性能的目的。而且这个场景通常不需要考虑离线消息这个头疼的问题.

### CS客服场景
以会话为中心的通信系统。系统的核心逻辑是基于会话的生命周期来设计，而聊天中的人与AI则是被调度的对象。

### 单聊
单聊以人为单位，而群聊以一批人为单位。
通常我们说的实时通信是指多方同时在线情况下，可以通过聊天服务实时收发消息，不过在IM这个场景中，极大可能出现一个用户A给另一个用户B发送消息时，用户B不在线，此时，消息就需要存储在服务器上；只要在设定的时间范围内，用户B登录到服务器，此消息就会同步到用户B，这就是离线消息。超过时间范围的消息就会被丢弃，如果不做离线同步或者同步逻辑有漏洞，就会导致消息丢失，这在业务上是零容忍的。

### 群聊
群的信息与成员列表通常是持久在数据库中，因为更新频率不高。
而会话（记录用户与连接的关系）随着用户的登录、退出、被踢、连接异常断开、自动重连等情况导致会经常变动，也就是大量的写入和删除操作，通常是存放在高速缓存中。

因此，这里的读取成员列表实际上是有两步：

从数据库中读取成员列表
从高速缓存中读取每个成员的登录会话信息
假设一个群成员有1千人，每一次消息转发，忽略消息持久化处理时长，仅读取成员列表和会话在性能上就是个考验。因此会话之类的信息是不可能保存在事务类的数据库中的。


### go
https://github.com/gobwas/ws