---
title: Google-drive-开发总结
date: 2022-03-24 14:16:28
tags:
---
>  Google Drive可以作为一些轻量级应用的存储系统，可以让用户登录Google Drive，用户数据就可以直接存Google Drive了

## 问题解决
### 避免用一个ip，短时间内，多个请求，我们可以看到官方文档的限制
- 通过配置和代码本身的控制，在允许的范围内，达到用户端的诉求
- https://stackoverflow.com/questions/29955680/raised-google-drive-api-per-user-limit-still-getting-userratelimitexceeded-erro
- https://stackoverflow.com/questions/25744367/google-drive-api-request-limitations
- https://www.reddit.com/r/PleX/comments/7oderc/google_drive_user_rate_limit_exceeded/