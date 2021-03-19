---
title: electron入门参考指北
date: 2021-03-03 18:52:07
tags:
    - electron
---
团队在electron方面的经验已经积累了2年多了，从较轻量级的客户端，到重量级的客户端；也不断有新同学想要学习或者加入相关项目的评审，这个时候回推荐一些相关的入门文档和demo,做个记录，之后可以直接扔链接了。


### demo day1
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

### 及时关注版本发布
https://www.electronjs.org/releases/stable
版本更新解决了什么问题
比如对M1芯片的支持，big sur的支持等～