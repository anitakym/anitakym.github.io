---
title: httpVersion-summary
date: 2022-12-09 16:11:21
tags:
---
- http://www.alloyteam.com/2016/07/httphttp2-0spdyhttps-reading-this-is-enough/
```
cite: 
对比 HTTPS 的升级改造，HTTP2.0 或许会稍微简单一些，你可能需要关注以下问题：

前文说了 HTTP2.0 其实可以支持非 HTTPS 的，但是现在主流的浏览器像 chrome，firefox 表示还是只支持基于 TLS 部署的 HTTP2.0 协议，所以要想升级成 HTTP2.0 还是先升级 HTTPS 为好。
当你的网站已经升级 HTTPS 之后，那么升级 HTTP2.0 就简单很多，如果你使用 NGINX，只要在配置文件中启动相应的协议就可以了，可以参考 NGINX 白皮书，NGINX 配置 HTTP2.0 官方指南。
使用了 HTTP2.0 那么，原本的 HTTP1.x 怎么办，这个问题其实不用担心，HTTP2.0 完全兼容 HTTP1.x 的语义，对于不支持 HTTP2.0 的浏览器，NGINX 会自动向下兼容的。
```
- https://http2.akamai.com/
```
https://caniuse.com/?search=http2
http://www.alloyteam.com/2015/03/http2-0-di-qi-miao-ri-chang/
```
- https://http3-explained.haxx.se/zh


- https://cloud.tencent.com/developer/article/1464264

- 腾讯云点播，如果想支持http2.0，发下需要配置的域名，腾讯云点播后台来配置就行，有个变更窗口了，需要下周一才能配置