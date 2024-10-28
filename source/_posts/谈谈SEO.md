---
title: 谈谈SEO
date: 2022-03-16 16:32:09
tags:
---
> 之前做的若干内部系统，不和搜索引擎打交道，尽量避免被收录，在nginx配置上面，可以增加避免的文件

### robots.txt
- https://developers.google.com/search/docs/advanced/robots/intro?hl=zh-cn
```
robots.txt 文件规定了搜索引擎抓取工具可以访问您网站上的哪些网址。 此文件主要用于避免您的网站收到过多请求；它并不是一种阻止 Google 抓取某个网页的机制。若想阻止 Google 访问某个网页，请使用 noindex 禁止将其编入索引，或使用密码保护该网页。
```
```
警告：如果您不想让自己的网页显示在 Google 搜索结果中，请不要将 robots.txt 文件用作隐藏网页的方法。

如果其他网页通过使用说明性文字指向您的网页，Google 在不访问您网页的情况下仍能将其网址编入索引。如果您想从搜索结果中屏蔽自己的网页，请改用其他方法，例如使用密码保护或 noindex。
```

### noindex
- https://developers.google.com/search/docs/advanced/crawling/block-indexing?hl=zh-cn
```
您可以通过在 HTTP 响应中包含 noindex 元标记或标头，阻止网页或其他资源显示在 Google 搜索中。当 Googlebot 下次抓取该网页并发现该标记或标头时，Google 就会完全阻止该网页出现在 Google 搜索结果中，不论是否有其他网站链接到该网页。
```
### Google
- https://developers.google.com/search
- https://seo.co/local-seo/
- https://moz.com/products/local
- https://www.google.com/business/
- https://trends.google.com/trends/?geo=HK
- https://ads.google.com/home/tools/keyword-planner/
- https://www.semrush.com/
- https://www.wordtracker.com/
- https://www.spyfu.com/

#### tips
- 去掉不好的link - https://support.google.com/webmasters/answer/2648487?hl=en
- `<rel='nofollow'>`
- 花钱
- metadata (title | description | keyword)
- facebook opengraph | twitter cards | pinterest rich pins - 去developer都可以查到文档
- 结构化的数据
- https://developers.google.com/search/docs/advanced/structured-data
- https://developers.google.com/search/docs/advanced/structured-data/breadcrumb
- https://developers.google.com/search/docs/advanced/structured-data/course

#### mobile
- manifest.json
- meta - viewport | fullscreen | balck status bar | home screen title
- https://github.com/cubiq/add-to-homescreen
- homescreen icons - add-to-homescreen


#### amp
- AMP is a web component framework to easily create user-first experiences for the web.
- https://amp.dev/

#### https
当然

#### 

#### https://ogp.me/
参与到 Open Graph Protocol 的好处：　

能够正确被蜘蛛抓取您的内容到百度网页搜索
帮助您的内容更有效的在百度结构化展现
应用了 OG 协议将会有更丰富的内容展现
- https://github.com/lorisleiva/vuepress-plugin-seo