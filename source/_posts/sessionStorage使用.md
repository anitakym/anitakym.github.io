---
title: sessionStorage使用
date: 2021-04-06 15:41:28
tags:
---
文档指路：https://developer.mozilla.org/zh-CN/docs/Web/API/Window/sessionStorage
书籍参考：高程=>23章 离线应用与客户端存储 => 23.3 数据存储 => 23.3.3 web存储机制

### Web Storage:
<pre>
WebStorage的目的是克服由cookie带来的一些限制，当数据需要被严格控制在客户端上时，无须持续地将数据发回服务器。
WebStorage的两个主要目标是：
提供一种在cookie之外存储会话数据的途径；
提供一种存储大量可以跨会话存在的数据的机制。

泽卡斯(Zakas. Nicholas C.). JavaScript高级程序设计(第3版) (图灵程序设计丛书) (Chinese Edition) (Kindle 位置 22327-22330). 人民邮电出版社. Kindle 版本. 

</pre>

!!!Storage类型只能存储字符串。非字符串的数据在存储之前会被转换成字符串。

sessionStorage对象是Storage的一个实例

sessionStorage对象应该主要用于仅针对会话的小段数据的存储。如果需要跨越会话存储数据，那么globalStorage或者localStorage更为合适。


应用场景：
1.对网页的崩溃进行监控
window对象：load && beforeunlaod事件
sessionStorage


window.addEventListener('load', () => {    sessionStorage.setItem('good_exit', 'pending') })
window.addEventListener('beforeunload', () => {    sessionStorage.setItem('good_exit', 'true') })
if(sessionStorage.getItem('good_exit') &&    sessionStorage.getItem('good_exit') !== 'true') {    // 捕 获 到⻚⾯崩溃 }


代码很 简单，思路 是 ⾸先 在⽹⻚ load 事件的回调 ⾥：利 ⽤ sessionStorage 记录 good_exit 值为 pending；接下来，在⻚⾯⽆异常退出前，即 beforeunload 事 件回调中，修改 sessionStorage 记录的 good_exit 值为 true。因此，如果⻚⾯ 没有崩溃的话，good_exit 值都会在离开前设置为 true，否则就可以通过 sessionStorage.getItem('good_exit') && sessionStorage.getItem('good_exit') !== 'true' 判断出⻚⾯崩溃，并进⾏处理。
框架的错误处理

如果你的应⽤部署了 PWA，那么便可以享受 service worker 带来的福利！在这 ⾥，可以通过 service worker 来完成⽹⻚崩溃的处理⼯作。基本原理在于： service worker 和⽹⻚的主线程独⽴。因此，即便⽹⻚发⽣了崩溃现象，也不会 影响 service worker 所在线程的⼯作。我们在监控⽹⻚的状态时，通过 navigator.serviceWorker.controller.postMessage API 来进⾏信息的获取和记 录。


HTML5 提供了两种在客户端存储数据的新方法：
	•	localStorage - 没有时间限制的数据存储
	•	sessionStorage - 针对一个 session 的数据存储


localStorage is similar to sessionStorage, except that while data stored in localStorage has no expiration time, data stored in sessionStorage gets cleared when the page session ends — that is, when the page is closed.


It should be noted that data stored in either localStorage or sessionStorage is specific to the protocol of the page.


1. Host
描述请求将被发送的目的地，包括，且仅仅包括域名和端口号。在任何类型请求中，request都会包含此header信息。
2. Origin
用来说明请求从哪里发起的，包括，且仅仅包括协议和域名。这个参数一般只存在于CORS跨域请求中，可以看到response有对应的header：Access-Control-Allow-Origin。
3. Referer
告知服务器请求的原始资源的URI，其用于所有类型的请求，并且包括：协议+域名+查询参数（注意，不包含锚点信息）。
因为原始的URI中的查询参数可能包含ID或密码等敏感信息，如果写入referer，则可能导致信息泄露。


A Storage object which can be used to access the current origin's local storage space.

The following snippet accesses the current domain's local Storage object and adds a data item to it using Storage.setItem().
localStorage.setItem('myCat', 'Tom');

The syntax for reading the localStorage item is as follows:
var cat = localStorage.getItem('myCat');

The syntax for removing the localStorage item is as follows:
localStorage.removeItem('myCat');

The syntax for removing all the localStorage items is as follows:
// clear all items
localStorage.clear();

#### localStorage 的封装lib
- store.js
 - https://github.com/marcuswestin/store.js
 - 浏览器兼容
 - 对字符串的处理（项目里面，如果不系统处理，在直接使用API的时候，每个人需要都处理一遍）
