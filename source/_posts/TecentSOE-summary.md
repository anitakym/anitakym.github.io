---
title: TecentSOE-summary
date: 2023-02-16 10:46:03
tags:
---
- https://cloud.tencent.com/document/product/884/86450
- https://cloud.tencent.com/document/product/884/103101
- https://aiedu.qcloud.com/soe/TencentSOE-0.1.4.js
- 没有开源，或者提供开发版文件，只能引入后debug调试看处理逻辑
```
使用过程中，您需要按照《智聆口语评测SDK合规使用指南》要求来使用，标注对应 SDK 信息，以下供参考：
第三方 SDK 名称：腾讯云智聆口语评测 SDK
第三方 SDK 提供方的公司名称：腾讯云计算（北京）有限责任公司
第三方 SDK 版本号：Android：1.2.3.119；iOS：1.2.3.114
使用目的及功能场景：中英文口语对话、教学、练习等场景 
处理的个人信息类型：Wi-Fi 状态、IP 地址、系统属性、设备型号、操作系统、相机、录音
实现 SDK 产品功能所需的权限：摄像头拍照、麦克风声音采集、网络、网络信息状态、读取外部存储、写入外部存储
第三方 SDK 隐私政策链接：https://cloud.tencent.com/document/product/884/71808
第三方 SDK 官网链接（可选披露）：https://cloud.tencent.com/document/product/884
处理方式（可选披露）：
1、采用 SSL 协议加密及 HTTPS 传输加密技术保障安全；
2、采取加密、去标识化等安全措施脱敏处理

```


### lame.all.js

Uncaught NetworkError: Failed to execute 'importScripts' on 'WorkerGlobalScope': The script at 'https://imgcache.qq.com/open/qcloud/soe/lame/lame.all.js' failed to load.

Lame.js 是 LAME 编码器的 JavaScript 版本。LAME 是一种广泛使用的 MP3 编码器。
Lame.js 可以把 WAV 音频转换为 MP3 格式。它能在浏览器环境运行，不需要安装任何插件
在一些需要实现语音记录、音频处理的网页应用中，常常会使用到 Lame.js。它可以获取用户的音频输入，处理并编码成 MP3 格式，然后上传到服务器或者进行其他处理。

```javascript
var mp3encoder = new lamejs.Mp3Encoder(1, 44100, 128);
var mp3Data = [];

Mixer.on('postSample', function(buffer) {
  var mp3buf = mp3encoder.encodeBuffer(buffer);
  if (mp3buf.length > 0) {
    mp3Data.push(mp3buf);
  }
});

Mixer.on('mixFinished', function() {
  var mp3buf = mp3encoder.flush();
  if (mp3buf.length > 0) {
    mp3Data.push(mp3buf);
  }
});
```
不过要注意，使用 Lame.js 需要遵循其相关的授权和使用条件，并且由于 LAME 编码器的特性，Lame.js 对浏览器的性能有一定的要求，可能不适合所有的环境和应用。

- https://imgcache.qq.com/open/qcloud/soe/lame/lame.all.js


importScripts会阻塞worker，直到所有的脚本都加载完成
如果load失败，主要原因是网络，会抛错，每日万次调用，个位数报错（1-2）


### lame
- https://sourceforge.net/projects/lame/
- LAME is an educational tool to be used for learning about MP3 encoding. The goal of the LAME project is to improve the psycho acoustics, quality and speed of MP3 encoding. Note: we provide source code only!
- LAME is a high quality MPEG Audio Layer III (MP3) encoder licensed under the LGPL.
- https://lame.sourceforge.io/
- 最新 LAME 版本：v3.100（2017 年 10 月）


- Lamejs 是对 Jump3R-Code （是对libmp3lame 的重写）的重写
- https://github.com/zhuker/lamejs


 Lamejs 是 LAME 项目（LAME Ain't an MP3 Encoder）的一种实现，此项目最初是用 C 语言编写的。Java 有一个开源库叫做 JLayer，它是 LAME 的 Java 实现（或者说，是 MPEG 1/2/2.5 audio Layer 1/2/3 的 Java 解码器）。

 ### github-https://github.com/zhuker/lamejs
 - 里面提供了Java对lame的实现版
 - worker-example提供了worker版的使用方式


 Web&微信H5
最近更新时间：2024-01-19 15:14:52

 
本页目录：
0.2.2 @ 2023.10.19
0.2.1 @ 2023.06.06
0.1.4 @ 2022.12.30
0.1.4 @ 2022.10.20
0.2.2 @ 2023.10.19
﻿点击下载 SDK﻿
新增参数
音频存储地址 cosBucketUrl
0.2.1 @ 2023.06.06
新增功能
新增 destroy 方法。用于解除麦克风占用。
0.1.4 @ 2022.12.30
新增功能
新增静音检测功能。
在 start 中新增 quiet 方法，用于检测用户是否连续处于静音状态。
在 start 中新增 volume 方法，用于检测当前音量。
新增参数
触发静音回调需要检测的连续的时间 TencentSOE.SilentDuration
低于该值，则认为是静音  TencentSOE.SilentVolume
0.1.4 @ 2022.10.20
Bug 及功能优化：
使用新的转发接口，提升请求效率。