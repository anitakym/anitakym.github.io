---
title: 游戏-cocos-design-arch-summary
date: 2023-11-08 15:23:14
tags:
---
### 存档功能


### 3.8.0->3.8.2
fix相关
`maxAudioChannel`是一个音频编程中常见的设置项，用于指定音频系统能够同时播放的音频流的最大数量，或者说，音频渠道的最大数量。例如，如果你设置 `maxAudioChannel` 为5，那么你的应用在同一时间内最多只能播放5个音频流。这个数量包括音乐和音效。

对 `maxAudioChannel` 的设置需要权衡性能和需求。如果设得过高，将会消耗更多的系统资源，可能会导致性能问题。但是如果设得过低，用户可能会因为无法同时听到所有的音频而有不良的体验。因此，在设置 `maxAudioChannel` 时，需要考虑到设备的性能限制以及应用的具体需求。


#### 
Fix the memory leak caused by excessive simultaneous playback of sound effects on the mini game platform #15541
修复小游戏平台音效同时播放过多导致内存泄漏的问题 #15541