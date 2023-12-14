---
title: IPFS-summary
date: 2023-12-11 10:13:46
tags:
---
Cloudflare IPFS Gateway 是一个公共的网关，允许你在没有安装IPFS（互联网文件系统）客户端的情况下访问存储在IPFS网络上的内容。IPFS是一种分布式文件系统，旨在创建持久且分布式存储和共享的文件。它是一种内容可寻址的方法，意味着它使用文件本身的哈希（一个唯一的数字指纹）来定位文件，而不是依赖于原始文件位置。

这个gateway的工作原理是：充当你和IPFS网络之间的代理。当你访问Cloudflare IPFS Gateway的网页时，Gateway将会在IPFS网络上寻找那个文件的哈希，并将内容提供给你。这使得任何连接到互联网的人都能查看IPFS上的内容，甚至他们自己没有运行IPFS节点。

这个服务也使得IPFS上的网站可以被搜索引擎索引，因为Cloudflare充当了一个可以被常规互联网访问的桥梁。同时，它也能为IPFS上的内容提供了DDOS保护。

需要注意的是，尽管你可以通过Cloudflare的IPFS Gateway访问IPFS网络，但是你不能将新的文件添加到IPFS网络上，除非你自己运行一个IPFS节点。 