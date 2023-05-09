---
title: bluetooth-miniprogram
date: 2022-07-18 12:00:27
tags:
---
https://zhuanlan.zhihu.com/p/405202290 - 抓包

## 蓝牙相关
### 蓝牙设备
- GATT 协议的低功耗设备 - 通过标准的 Web Bluetoot h API 进行通信，而 Chrome 浏览器已经支持了这个 API，所以我们可以直接使用这个 API 进行通信。
- SPP 协议的设备 - 不能直接使用 Web Bluetooth API 进行通信，需要通过 Node.js 来实现一个蓝牙串口服务，然后通过这个服务来进行通信。

- SPP 协议是一种基于串口的蓝牙通讯协议，它的特点是：

串口通讯协议，即数据以字节流的形式传输，没有数据帧的概念。
通讯速率较低，一般为 9600bps。
通讯距离较短，一般为 10 米以内。
 
通讯稳定性较高，一般不会出现数据丢失的情况。
通讯延迟较低，一般为 10ms 以内。
- https://github.com/tinyprinter/node-bluetooth-serial-port


## 封装基类
- Bluetooth