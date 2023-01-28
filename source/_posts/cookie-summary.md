---
title: cookie-summary
date: 2023-01-20 23:07:44
tags:
---
> 之前好多文章也提过cookie，基于它的工作中问题的解决，浏览器相关的why,what,how


### 减少cookie
- 问题：旧项目，页面打开问题，cookie过大，页面跳转携带cookie，网络较差情况下，cookie会导致出现空白
- 浏览器对cookie大小的限制（不同浏览器不一样），服务侧对header大小的限制（看配置）
- 策略： 主站设置白名单｜定期删除非白名单cookie
- 好处：减少页面间传输大小｜对cookie进行有效管理