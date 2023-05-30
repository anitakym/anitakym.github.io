---
title: DNS解析
date: 2021-03-10 10:44:15
tags:
    - tencent-cloud
    - DNS
---

> 由腾讯云的DNSPod文档讲起

文档指南：
https://cloud.tencent.com/document/product/302/3449

各记录类型的设置：
- 通过添加 A 记录可将域名指向一个 IP 地址（外网地址）
- 如果需要将域名指向另一个域名，再由另一个域名提供 IP 地址，就需要添加 CNAME 记录，最常用到 CNAME 的场景包括做 CDN、做企业邮箱。
- 如果需要设置邮箱，让邮箱能收到邮件，就需要添加 MX 记录。
- 如果需要将子域名交给其他 DNS 服务商解析，则需要添加 NS 记录。
- 通过添加 AAAA 记录可将域名指向一个 IPv6 地址。
- SRV 记录用来标识某台服务器使用了某个服务，常见于微软系统的目录管理。
- 如果希望对域名进行标识和说明，可以使用 TXT 记录，绝大多数的 TXT 记录是用来做 SPF 记录（反垃圾邮件）。
- 将一个域名指向另外一个已经存在的站点时，需要添加 URL 记录。
  - 隐性转发：用的是 iframe 框架技术、非重定向技术，效果为浏览器地址栏输入 http://a.com 回车，打开网站内容是目标地址 http://cloud.tencent.com/ 的网站内容，但地址栏显示当前地址 http://a.com 。
  - 显性转发：用的是301重定向技术，效果为浏览器地址栏输入 http://a.com 回车，打开网站内容是目标地址 http://cloud.tencent.com/ 的网站内容，且地址栏显示目标地址 http://cloud.tencent.com/。
  - 添加 URL 转发记录时，涉及到的两个域名已完成备案。未经备案的域名无法添加 URL 转发。
  - 备案内容要和Document title一致

  ### 传统DNS
  - 域名缓存
  - 域名转发
  - 出口NAT（网络地址转换）
  - 域名更新


  ### HTTPDNS
  #### 应用场景
  - 手机端嵌入SDK
  - 解决本地DNS服务缓存更新不及时的问题

  #### 设计
  - 缓存设计
    - 客户端SDK，本地缓存，HTTPDNS服务器
    - 缓存的过期，更新，不一致的问题
    - 同步更新-Cache-Aside
    - 异步更新-Refresh-Ahead （Guava Cache）
  - 调度设计
  #### cases
  - https://juejin.cn/post/7200278589874782265


 #### dig
 查DNS的问题
 一般做了CDN缓存，可以用这个看看，或者新上的域名，运维配置有没有问题；