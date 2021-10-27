---
title: 几个ip地址的含义
date: 2021-04-14 17:05:35
tags:
---

对于监听地址， :: 等同于IPV4的0.0.0.0 （全0）
而 ::1 则等同于 127.0.0.1 （本机地址）

在IP地址范围内，一部分地址将保留作为私人IP地址空间，专门用于内部局域网使用，这些地址如下表：

  A类 10.0.0.0-10.255.255.255 网络数：1
  B类 172.16.0.0-172.31.255.255 网络数：16
  C类 192.168.0.0-192.168.255.255 网络数：255

  这些地址是不会被Internet分配的，它们在Internet上也不会被路由，虽然它们不能直接和Internet网连接，但通过技术手段仍旧可以和Internet通讯。我们可以根据需要来选择适当的地址类，在内部局域网中将这些地址像公用IP地址一样地使用。在Internet上，有些不需要与Internet通讯的设备，如打印机、可管理集线器等也可以使用这些地址，以节省IP地址资源。

// Various Dev Server settings
    host: '10.200.166.65', // can be overwritten by process.env.HOST
    port: 8887, // can be overwritten by process.env.PORT, if port is in use


起服务的时候：
用本机ip,或者0.0.0.0
这样子局域网的别的机器才能访问(局域网地址)到

https://applegazette.com/mac/what-is-localhost-and-how-is-it-different-from-127-0-0-1/


https://stackoverflow.com/questions/20778771/what-is-the-difference-between-0-0-0-0-127-0-0-1-and-localhost/20778887#20778887

127.0.0.1 is normally the IP address assigned to the "loopback" or local-only interface. This is a "fake" network adapter that can only communicate within the same host. It's often used when you want a network-capable application to only serve clients on the same host. A process that is listening on 127.0.0.1 for connections will only receive local connections on that socket.

"localhost" is normally the hostname for the 127.0.0.1 IP address. It's usually set in /etc/hosts (or the Windows equivalent named "hosts" somewhere under %WINDIR%). You can use it just like any other hostname - try "ping localhost" to see how it resolves to 127.0.0.1.

0.0.0.0 has a couple of different meanings, but in this context, when a server is told to listen on 0.0.0.0 that means "listen on every available network interface". The loopback adapter with IP address 127.0.0.1 from the perspective of the server process looks just like any other network adapter on the machine, so a server told to listen on 0.0.0.0 will accept connections on that interface too.

At least in Windows, localhost behaves as 0.0.0.0 (not 127.0.0.1) by default


https://gist.github.com/zxhfighter/b9f4b4ef328cd8b433b0e9dc2f4af26d

实际测试：
均为Mac

127.0.0.1 起服务，同局域网的另外一台Mac无法访问-ERR_CONNECTION_REFUSED
0.0.0.0 起服务，同局域网的另外一台Mac可以访问 # 注意，开启VPN的情况下，可能会导致访问出问题；


### mongo 安全事件
https://www.jianshu.com/p/d34ff415fbb4


### 一个有趣的小白用户讨论
https://github.com/gruntjs/grunt-contrib-connect/issues/164
