---
title: webkit-bug-report
date: 2024-02-21 10:43:56
tags:
---

### 涉及获取摄像头获取视频和麦克风获取音频流的业务
https://bugs.webkit.org/buglist.cgi?quicksearch=OverConstrainedError
https://bugs.webkit.org/show_bug.cgi?id=176349
- sentry收到报错，只有一条，设备信息为macos，Safari浏览器

- https://itecnote.com/tecnote/javascript-how-to-resolve-ios-11-safari-getusermedia-invalid-constraint-issue/

- https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getDisplayMedia#%E5%BC%82%E5%B8%B8
- MediaDevices.getDisplayMedia()


### createStream
- https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createStream
```
createStream(streamConfig) → {Stream}
创建一个本地流 Stream 对象，本地流 Stream 对象通过 publish() 方法发布本地音视频流。

注意：一个音视频流 Stream 中最多只能包含一个音频 track 和一个视频 track。

本地音视频流可以

从摄像头和麦克风采集获得，适用于一般的音视频通话。
从屏幕分享源采集获得，适用于进行屏幕分享。
从开发者通过 audioSource/videoSource 指定的 MediaStreamTrack 获得， 使用这种方式业务层可先对音视频进行前处理，比如，对音频进行混音，或者对视频进行美颜处理，亦或者通过这种方式向远端用户推送一个正在播放的音视频文件。

```