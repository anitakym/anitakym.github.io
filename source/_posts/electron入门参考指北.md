---
title: electron入门参考指北
date: 2021-03-03 18:52:07
tags:
    - electron
---
团队在electron方面的经验已经积累了2年多了，从较轻量级的客户端，到重量级的客户端；也不断有新同学想要学习或者加入相关项目的评审，这个时候回推荐一些相关的入门文档和demo,做个记录，之后可以直接扔链接了。

### 安装网络问题
```
RequestError: socket hang up
    at ClientRequest.<anonymous> 
    at Object.onceWrapper (events.js:483:26)
    at ClientRequest.emit (events.js:388:22)
    at ClientRequest.origin.emit 
    at TLSSocket.socketOnEnd (_http_client.js:499:9)
    at TLSSocket.emit (events.js:388:22)
    at endReadableNT (internal/streams/readable.js:1336:12)
    at processTicksAndRejections (internal/process/task_queues.js:82:21)
```
- 保证网络即可

### learning-intro
- https://electronjs.org/docs
文档啦，关于看文档，这儿推荐一本书，叫《如何阅读一本书》，讲得就是如何阅读的，其实我们好多人的阅读能力还停留在小学六年级水平，看了这本书，还是大有裨益。
- https://github.com/electron/electron-api-demos
结合文档，跑一遍这个demo,对能做什么，做成什么样，就会有很直观的认知（electron官方出的）
- electron fiddle https://www.electronjs.org/fiddle
也是官方出的，可以试用功能，改代码查看功能，可以看看代码是否能在electron指定的版本上面运行
- TIPS:
  - webPreferences.nodeIntegration 这个选项的关闭还是开启需要注意（安全问题）_https://www.electronjs.org/docs/tutorial/security ,可以按照官方说明进行处理.
      - ⚠️ Under no circumstances should you load and execute remote code with Node.js integration enabled. Instead, use only local files (packaged together with your application) to execute Node.js code. To display remote content, use the <webview> tag or BrowserView, make sure to disable the nodeIntegration and enable contextIsolation.
  - 如果开启了nodeIntegration，用<script>引入jQuery就会有问题， jQuery内部会对require变量判断，和node的require冲突；所以只能
    ```
    window.$ = window.jQuery = require('./jquery-3.5.1.min)
    ```
新版本不可  <script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
旧版本可以  <script src="https://cdn.bootcdn.net/ajax/libs/jquery/1.4.1/jquery.min.js"></script>
```
$.fn.jquery
1.4.1
$.fn.jquery
VM338:1 Uncaught TypeError: Cannot read property 'jquery' of undefined
    at <anonymous>:1:6
```

### log
#### electron-log
文档：https://github.com/megahertz/electron-log
By default, it writes logs to the following locations:

on Linux: ~/.config/{app name}/logs/{process type}.log
on macOS: ~/Library/Logs/{app name}/{process type}.log
on Windows: %USERPROFILE%\AppData\Roaming\{app name}\logs\{process type}.log

可以引入之后再封装一层
### 及时关注版本发布
https://www.electronjs.org/releases/stable
版本更新解决了什么问题
比如对M1芯片的支持，big sur的支持等～


### 网络问题判断
online
offline
网络状态不好有两种情况：
1. 切断物理连接本身
2. 网络本身有问题(如路由等具体问题)
嗯呢，navigator.onLine不完全可靠，无法检测网络真实状态，只能判断是否是物理切断连接
通用更可靠方案是：定时向服务器发起任意一个能够判断网络状态的请求，类似心跳连接

Unfortunately, these events aren't fully reliable. If you need greater reliability, or if the API isn't implemented in the browser, you can use other signals to detect if you are offline including using service workers and responses from XMLHttpRequest.
————————————————————————
https://developer.mozilla.org/en-US/docs/Web/API/NavigatorOnLine/Online_and_offline_events

https://github.com/sindresorhus/is-online

https://www.electronjs.org/docs/tutorial/online-offline-events


### sentry - error
- Error: EBUSY: resource busy or locked
```
The main reason you are seeing this error is due to a program putting a lock on the folder for whatever reason. Testing the command while closing programs one at a time can help resolve the issue and let you know which program is the culprit.
One issue people were having was with anti-malware on windows. You can read through this thread here:
https://github.com/npm/npm/issues/13461
In case link stops working here was the most upvoted comment:
In Windows 10 64-bit OS, I have resolved this issue by uninstalling Anti-Malware software. - 卸载杀毒软件
Another way you can trigger this error is if you are running an npm run [command] while cd'd into the directory that its altering. This happened to me where I closed every program and it didn't work, but realized I was inside the dist folder which needed to be removed and rebuilt. This triggered the Error: EBUSY: resource busy or locked, rmdir error in PowerShell and can be reproduced every time.
```

### Preload
webPreferences-preload
(https://www.electronjs.org/docs/api/browser-window)


### download
我们项目中基于downloadItem实现的
可以看看这个项目（@electron/get）的实现https://github.com/electron/get

### 安装背景图
如果想要背景清楚，可以用二倍图，文件命名符合规则即可生效
<pre>
Adopt the @2x Naming Convention
When you create a high-resolution version of an image, follow this naming convention for the image pair:

Standard: <ImageName>.<filename_extension>
Example: circle.png

High resolution: <ImageName>@2x.<filename_extension>
Example: circle@2x.png

The <ImageName> and <filename_extension> portions specify the name and extension for the file. The inclusion of the @2x modifier for the high-resolution image lets the system know that the image is the high-resolution variant of the standard image. The two component images should be in the same folder in the app’s sources. Ideally, package the image pairs into one file (see Package Multiple Versions of Image Resources into One File).
</pre>


### 可参考他人踩坑文档
https://www.yuque.com/arvinxx-fe/electron
本质还是项目中遇到问题，解决问题，有空了彻底解决问题


### app-builder
- https://www.npmjs.com/package/app-builder-bin

```
app-builder
Generic helper tool to build app in a distributable formats. Used by electron-builder but applicable not only for building Electron applications
```
- https://github.com/electron-userland/electron-builder
```
和node的版本有关 - 16.X的时候
reify:app-builder-bin: timing reifyNode:node_modules/typescript Completed in 6782ms
```

## feature
#### -webkit-app-region
- https://github.com/electron/electron/issues/1354
- https://www.electronjs.org/zh/docs/latest/api/frameless-window
- 父元素设置了，子元素不想，可以重新设置下子元素的这个属性

#### window
- 适时显示窗口
- 不规则窗口的设置
- 点击穿透透明区域 - trick
- 多窗口资源竞争问题 （渲染进程通信 - node-fs.watch - token令牌来控制文件读写）
- 模态窗口

#### Mac｜win
- process.versions.electron
- nativeTheme.shouldUseDarkColors

#### webContents
- 监听页面事件
- 页面加载时间 ｜ 页面跳转事件-navigate|redirect
- webFrame - 访问和控制子页面的对象
- getFoucusedWebContents

#### Canvas|Svg
- Canvas - 较小的画布上绘制大量元素，较强的频繁重绘能力 - 当绘制元素超出画布大小之后，绘制工作不再占用渲染资源
- Svg - 大型渲染区域绘制少量元素，或者需要复杂事件交互逻辑的图形
- Canvas - 线条变粗且颜色变淡的现象 - 计算机最小1px - 解决方案，宽度增加或者减少0.5个像素
- PixiJS库