---
title: network-information-API-summary
date: 2024-03-06 10:20:53
tags:
---
https://googlechrome.github.io/samples/network-information/
https://github.com/googlechrome/samples/tree/gh-pages/network-information
```
type: undefined
     downlink: 1.45 Mb/s
          rtt: 300 ms
  downlinkMax: undefined Mb/s
effectiveType: 4g
     saveData: false
```
Network Information API 提供了有关系统网络连接的信息，允许 Web 应用程序在网络连接改变时访问并适应这些变化。这个 API 提供的信息有以下几个主要参数：

type: 这是一个表示用户设备网络连接类型的字符串。它可以是 bluetooth，cellular，ethernet，none，wifi，wimax，other，unknown。

effectiveType: 这是一个表示用户设备的有效网络连接类型的字符串，主要考虑带宽和网络延迟。它可以是 slow-2g，2g，3g，4g。

downlink: 这是一个表示设备的下行速度（单位：Mbps，向用户设备发送数据的速度）的数值。

uplink: 表示设备的上行速度（单位：Mbps，用户设备发送数据的速率）。

rtt: 这是代表用户设备网络连接的往返时间（以毫秒为单位）的数字。被用来估计网络的延迟。

saveData: 这是一个表示用户设备是否在尽量减少数据使用的布尔值，它是根据用户的浏览器设置和操作系统设置决定的。