---
title: python-flask-聊聊设计思想
date: 2021-12-01 16:20:47
tags:
---
> https://dormousehole.readthedocs.io/en/latest/

### doc
- https://github.com/pallets/flask

## notes

### Jinjia2 

Time 问题

### py 2->3
其中提到如下:在py3之后，引入方式已经发生了改变
from flask.ext.wtf import Form

解决办法: 改变引入方式为:
from flask_wtf import Form

### http
重定向 经常 使用 302 状态 码表 示， 指向 的 地址 由 Location 首部 提供。 重定向 响应 可以 使用 3 个 值 形式 的 返回 值 生成， 也可 在 Response 对象 中 设定。 不过， 由于 使用 频繁， Flask 提供 了 redirect() 辅助 函数，

格林布戈(Miguel Grinberg). Flask Web开发 基于Python的Web应用开发实战 (图灵程序设计丛书) (p. 14). 人民邮电出版社. Kindle 版本.
定义如下：
301 Moved Permanently 被请求的资源已永久移动到新位置，并且将来任何对此资源的引用都应该使用本响应返回的若干个URI之一。如果可能，拥有链接编辑功能的客户端应当自动把请求的地址修改为从服务器反馈回来的地址。除非额外指定，否则这个响应也是可缓存的。

302 Found 请求的资源现在临时从不同的URI响应请求。由于这样的重定向是临时的，客户端应当继续向原有地址发送以后的请求。只有在Cache-Control或Expires中进行了指定的情况下，这个响应才是可缓存的。
字面上的区别就是301是永久重定向，而302是临时重定向。 当然，他们之间也是有共同点的，就是用户都可以看到url替换为了一个新的，然后发出请求。
 
 
301适合永久重定向
　　301比较常用的场景是使用域名跳转。
　　比如，我们访问 http://www.baidu.com 会跳转到 https://www.baidu.com，发送请求之后，就会返回301状态码，然后返回一个location，提示新的地址，浏览器就会拿着这个新的地址去访问。 
　　注意： 301请求是可以缓存的， 即通过看status code，可以发现后面写着from cache。
　    或者你把你的网页的名称从php修改为了html，这个过程中，也会发生永久重定向。
 
 
302用来做临时跳转
　　比如未登陆的用户访问用户中心重定向到登录页面。
　　访问404页面会重新定向到首页。 
##niginx 301/302配置
rewrite后面接上permenent就代表301跳
//把来自veryyoung.me的请求301跳到 www.veryyoung.me
if ($host != 'veryyoung.me') {
    rewrite ^/(.*)$ http://www.veryyoung.me/$1 permanent;
}
 
接上redirect就代表302跳
//把来自veryyoung.me的请求302跳到 www.veryyoung.me
if ($host != 'veryyoung.me') {
    rewrite ^/(.*)$ http://www.veryyoung.me/$1 redirect;
}
 
 
301重定向和302重定向的区别
　　302重定向只是暂时的重定向，搜索引擎会抓取新的内容而保留旧的地址，因为服务器返回302，所以，搜索搜索引擎认为新的网址是暂时的。
　　而301重定向是永久的重定向，搜索引擎在抓取新的内容的同时也将旧的网址替换为了重定向之后的网址。

### 枚举
可读性比数字强


### 如果要注册视图函数，要实例化一个函数红图对象


### 关于用户的思考
- 不仅仅人
- API ，开放性，通用性
- 装饰器


### REST

### wtforms
http://wtforms.simplecodes.com/docs/0.6/index.html