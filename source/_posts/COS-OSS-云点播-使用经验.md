---
title: COS-OSS-云点播-使用经验
date: 2022-06-30 17:16:05
tags:
---

```
https://cloud.tencent.com/document/product/436/31315
通过互联网测试的说明
由于通过互联网访问 COS 会经过运营商网络，运营商网络可能禁止您使用 ICMP 协议的ping或traceroute等工具来测试连通性，因此建议使用 TCP 协议的工具来测试连通性。

注意：
通过互联网访问可能受到多种网络环境的影响，如有访问不畅的情况，请排查本地网络链路或联系当地运营商进行反馈。

若您的运营商允许 ICMP 协议，您可以使用ping、traceroute或mtr工具来检视您的链路状况。运营商不允许使用 ICMP 协议，您可以使用psping（Windows 环境，请前往微软官网下载）或tcping （跨平台软件）等工具进行时延测试。

通过内网测试的说明
如果您通过同地域的腾讯云 VPC 网络来访问对象存储 COS，则可能无法使用 ICMP 协议的ping或traceroute等工具来测试连通性。建议您使用基本连通测试中的telnet命令进行测试。

您亦可尝试使用psping或tcping等工具直接对访问域名的80端口进行时延测试，请在测试前确保已通过nslookup命令查询并确认访问域名已正确解析至内网地址。
```