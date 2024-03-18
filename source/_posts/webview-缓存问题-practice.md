---
title: webview-缓存问题-practice
date: 2023-11-14 16:56:52
tags:
---
https://www.geeksforgeeks.org/write-through-and-write-back-in-cache/

- 在一个客户端 App 中，多个 WKWebView 使用中会共享一个 UI 进程(与 App 进程共享)、共享一个 Networking 进程、每个 WKWebView 实例独享一个 WebContent 进程
- A WKProcessPool object represents a single process that WebKit uses to manage web content. To provide a more secure and stable experience, WebKit renders the content of web views in separate processes, rather than in your app’s process space. By default, WebKit gives each web view its own process space until it reaches an implementation-defined process limit. After that, web views with the same WKProcessPool object share the same web content process.(WebContent 进程启动规则 - <ios13)

### 线程终止问题
### wbwebviewmemory
- webViewWebContentProcessDidTerminate
- https://github.com/fuyoufang/WKWebViewMemory


## WKWebView 请求拦截探索与实践

https://juejin.cn/post/6922625242796032007/
https://juejin.cn/post/7099004308120666120

## GCDWebServer