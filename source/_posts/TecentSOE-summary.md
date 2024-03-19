---
title: TecentSOE-summary
date: 2023-02-16 10:46:03
tags:
---
- https://aiedu.qcloud.com/soe/TencentSOE-0.1.4.js
- 没有开源，或者提供开发版文件，只能引入后debug调试看处理逻辑


### lame.all.js

Uncaught NetworkError: Failed to execute 'importScripts' on 'WorkerGlobalScope': The script at 'https://imgcache.qq.com/open/qcloud/soe/lame/lame.all.js' failed to load.

Lame.js 是 LAME 编码器的 JavaScript 版本。LAME 是一种广泛使用的 MP3 编码器。

简单来说，Lame.js 可以把 WAV 音频转换为 MP3 格式。它能在浏览器环境运行，不需要安装任何插件，这为在 Web 环境中处理音频提供了极大的便利。

比如在一些需要实现语音记录、音频处理的网页应用中，常常会使用到 Lame.js。它可以获取用户的音频输入，处理并编码成 MP3 格式，然后上传到服务器或者进行其他处理。

下面是一个简单的 Lame.js 使用示例：

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

如果load失败，主要原因是网络，会抛错，每日万次调用，个位数报错（1-2）