---
title: HTTP相关问题
date: 2018-09-17 18:43:51
tags:
  - HTTP
---

## History



## TCP
> 连接是两端的状态维护
> 连接的断开比建立略微复杂，因为资源的constructor比destructor要简单（因为destructor要考虑所有资源的安全有序释放）
## 基础
### 结构
报文：
- 请求行 （POST /good HTTP/1.1）
- 请求首部
- 请求的正文实体

HTTP请求的报文好了之后，浏览器或者移动端APP会把它交给传输层
- Socket
- 浏览器 ｜ 移动端-HTTP客户端工具
- HTTP 基于TCP，面向连接的方式发送请求，基于Stream二进制流的方式传送，到了TCP层，会把二进制流变成一个报文段发送给服务器
- TCP头｜IP头
## 状态码

#### 502网关问题
#### 415（unsupported media type）（content-type）
415 Unsupported Media Type 是一种HTTP协议的错误状态代码，表示服务器由于不支持其有效载荷的格式，从而拒绝接受客户端的请求。

格式问题的出现有可能源于客户端在 Content-Type 或 Content-Encoding 首部中指定的格式，也可能源于直接对负载数据进行检测的结果。

Java

500 内部报错

#### 503 service unavailable

服务端错误状态码，表示服务器尚未处于可以接受请求的状态

通常造成这种情况的原因是由于服务器停机维护或者已超载。注意在发送该响应的时候，应该同时发送一个对用户友好的页面来解释问题发生的原因。该种响应应该用于临时状况下，与之同时，在可行的情况下，应该在 Retry-After 首部字段中包含服务恢复的预期时间。
缓存相关的首部在与该响应一同发送时应该小心使用，因为 503 状态码通常应用于临时状况下，而此类响应一般不应该进行缓存。

cite(https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/503)

#### 204
- 204 No Content
- 只需要返回成功与否，204可以节约多余的数据传输
- DELETE ｜ 客户端上传端信息给服务器，不关心相应
- http://clients1.google.com/generate_204

#### 414
- https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/414
- 414 URI Too Long
```
当客户端误将 POST 请求当作 GET 请求时，会带有一个较长的查询字符串(query)；
当客户端堕入重定向循环黑洞时，例如，指向自身后缀的重定向URI前缀(a redirected URI prefix that points to a suffix of itself)；
当客户端对服务器进行攻击，试图寻找潜在的漏洞时。
```

## 相关库

### axios
文档指南，各种用法（https://github.com/axios/axios#axios-api）
#### Features（支持Promise API）
- Make XMLHttpRequests from the browser(从浏览器中创建 XMLHttpRequests)
- Make http requests from node.js(从 node.js 创建 http 请求)
- Supports the Promise API(支持 Promise API)
- Intercept request and response(拦截请求和响应)
- Transform request and response data(转换请求数据和响应数据)
- Cancel requests(取消请求)
- Automatic transforms for JSON data(自动转换 JSON 数据)
- Client side support for protecting against XSRF(客户端支持防御 XSRF)
- 不支持IE（11及以下）

#### Cancellation
You can cancel a request using a cancel token.

The axios cancel token API is based on the withdrawn cancelable promises proposal.

You can create a cancel token using the CancelToken.source factory as shown below:
```
const CancelToken = axios.CancelToken;
const source = CancelToken.source();

axios.get('/user/12345', {
  cancelToken: source.token
}).catch(function (thrown) {
  if (axios.isCancel(thrown)) {
    console.log('Request canceled', thrown.message);
  } else {
    // handle error
  }
});

axios.post('/user/12345', {
  name: 'new name'
}, {
  cancelToken: source.token
})

// cancel the request (the message parameter is optional)
source.cancel('Operation canceled by the user.');
You can also create a cancel token by passing an executor function to the CancelToken constructor:

const CancelToken = axios.CancelToken;
let cancel;

axios.get('/user/12345', {
  cancelToken: new CancelToken(function executor(c) {
    // An executor function receives a cancel function as a parameter
    cancel = c;
  })
});

// cancel the request
cancel();
```
Note: you can cancel several requests with the same cancel token.

* example
```
const CancelToken = axios.CancelToken
const pending = []
const defaultConfig = {}

defaultConfig.cancelToken = new CancelToken(function executor(c) {
  pending.push(c)
})

// 需要避免多次请求的时候执行下面代码
while (pending.length > 0) {
  pending.pop()('请求中断')
}
```
## CORS
- Fetch/XMLHTTPRequest都遵循同源策略
- https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS
#### preflighted requests
- https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/OPTIONS
- 浏览器发起的预检请求 - 为了防止对服务器数据产生副作用的请求方法，浏览器会用OPTIONS方法发起一个预检请求，获知服务器是否允许这个跨域请求，允许就发送真实请求，不允许，则阻止真实请求；
- Method: OPTIONS
```
* It uses methods other than GET, HEAD or POST. Also, if POST is used to send request data with a Content-Type other than application/x-www-form-urlencoded, multipart/form-data, ortext/plain, e.g. if the POST request sends an XML payload to the server using application/xmlor text/xml, then the request is preflighted.
* It sets custom headers in the request (e.g. the request uses a header such as X-PINGOTHER)
```
```
跨域资源共享标准（ cross-origin sharing standard ）允许在下列场景中使用跨域 HTTP 请求：
	•	前文提到的由 XMLHttpRequest 或 Fetch 发起的跨域 HTTP 请求。
	•	Web 字体 (CSS 中通过 @font-face 使用跨域字体资源), 因此，网站就可以发布 TrueType 字体资源，并只允许已授权网站进行跨站调用。
	•	WebGL 贴图
	•	使用 drawImage 将 Images/video 画面绘制到 canvas
```

## GET 
### URL长度
- Http Get方法提交的数据大小长度并没有限制，HTTP协议规范没有对URL长度进行限制。这个限制是特定的浏览器及服务器对它的限制。
```
net::ERR_CONNECTION_RESET 200
https://spectrum.imgix.net/communities/8f3cb70e-0b51-4c7b-8a69-3d27f1c16887/logo-grid.png.0.393240430324705?w=1280&h=384&dpr=2&q=100&expires=1573084800000&ixlib=js-1.4.1&s=74b9ab44b425ebcfd87e1e0b1af56d8b
```
#### 说明
GET请求限制传递参数长度为2k，长度过长会重置连接（只有IE）
下面就是对各种浏览器和服务器的最大处理能力做一些说明
Microsoft Internet Explorer (Browser)
IE浏览器对URL的最大限制为2083个字符，如果超过这个数字，提交按钮没有任何反应。Firefox (Browser)
对于Firefox浏览器URL的长度限制为65,536个字符。
Safari (Browser)
URL最大长度限制为 80,000个字符。
Opera (Browser)
URL最大长度限制为190,000个字符。
Google (chrome)
URL最大长度限制为8182个字符。
Apache (Server)
能接受最大url长度为8,192个字符。
Microsoft Internet Information Server(IIS)
能接受最大url的长度为16,384个字符。

### cacheable
- https://developer.mozilla.org/en-US/docs/Glossary/Cacheabl
```
A cacheable response is an HTTP response that can be cached, that is stored to be retrieved and used later, saving a new request to the server. Not all HTTP responses can be cached, these are the following constraints for an HTTP response to be cached:
	•	The method used in the request is itself cacheable, that is either a GET or a HEAD method. A response to a POST or PATCH request can also be cached if freshness is indicated and the Content-Location header is set, but this is rarely implemented. (For example, Firefox does not support it per https://bugzilla.mozilla.org/show_bug.cgi?id=109553.) Other methods, like PUT or DELETE are not cacheable and their result cannot be cached.
	•	The status code of the response is known by the application caching, and it is considered cacheable. The following status code are cacheable: 200, 203, 204, 206, 300, 301, 404, 405, 410, 414, and 501.
	•	There is no specific headers in the response, like Cache-Control, that prevents caching.
Note that some non-cacheable requests/responses to a specific URI may invalidate previously cached responses on the same URI. For example, a PUT to pageX.html will invalidate all cached GET or HEAD requests to the same URI.
When both, the method of the request and the status of the response, are cacheable, the response to the request can be cached:
GET /pageX.html HTTP/1.1
(…) 

200 OK
(…)


A PUT request cannot be cached. Moreover, it invalidates cached data for request to the same URI done via HEAD or GET:
PUT /pageX.html HTTP/1.1
(…)

200 OK
(…)

A specific Cache-Control header in the response can prevent caching:
GET /pageX.html HTTP/1.1
(…)

200 OK
Cache-Control: no-cache
(…)
```
- 206 - https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status/206 - Partial Content
- The 206 (Partial Content) status code indicates that the server is successfully fulfilling a range request for the target resource by transferring one or more parts of the selected representation that correspond to the satisfiable ranges found in the request's Range header field (Section 3.1).

## HTTPS - SSL

可见“升https”博文

### Connection
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Keep-Alive
- (HTTP/2 does not use the Connection header field to indicate
   connection-specific header fields)


## JSON
```
JS object notation

轻量级的数据交换格式
相对于xml非常轻

字符串是JSON的表现形式

符合JSON格式的字符串叫JSON字符串

XML

JSON 易于阅读，解析，网络传输效率高，跨语言交换数据

把语言写的东西做成服务，调用服务提供数据

import json

json.loads(json_Str)

Json字符串对应到python
字典

JSON object,array

数组其实就是一个集合

由字符串到某个语言下的数据结构（反序列化）

Json			python
object	dict
array			list
string	str
number 	int
number	float
true			True
false		False
null			None

一种语言是其它语言的语法糖
很多是C的语法糖
语言就是一种工具

序列化
Json.dumps()

终端其实看不大出来是不是字符串


序列化之后直接存到mysql不太好，还是要弄成对象数据结构存，nosql(mongo) 可以存序列化之后的

JSON 对象 （放在js中是成立的，但是放在python中，是没有的）
JSON
JSON 字符串

JSON 也是ecmascirpt的一个实现




A              					JSON                 				B
A语言的数据类型		JSON数据类型（中间数据类型）	B语言的数据类型

JSON有自己的数据类型，虽然它和javascirpt的数据类型有些相似

REST服务的标准格式（JSON）

```

### 301 302

HTTP状态码301和302都是重定向代码，但它们在使用场景上会有所不同：

- 301 Moved Permanently：这是一个永久重定向，意味着资源已被永久移动至新的位置。你应该在以下场景使用301重定向：
  - 当网站的URL结构被修改，原来的URL并不再使用时。
  - 如果你的网站从HTTP升级到HTTPS。
  - 如果你有两个相似的网页，并希望将其中一个合并到另一个页面，301重定向可以让你有效地将访问量和搜索引擎等级传递给新的页面。
- 302 Found (HTTP 1.1) / Moved Temporarily (HTTP 1.0)：这是一个临时重定向，表示资源被临时移动到了新的位置，但在将来可能会返回到原来的位置。你应该在以下场景使用302重定向：
  - 当你的网站或某个特定页面正在进行维护，你希望用户暂时访问备用页面时。
  - 当进行A/B测试以分析网页性能时。

在所有这些情况中，重定向均确保了用户能够找到他们试图访问的页面，同时保持页面的搜索引擎排名。