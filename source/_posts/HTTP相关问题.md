---
title: HTTP相关问题
date: 2018-09-17 18:43:51
tags:
  - HTTP
---

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
#### preflighted requests
- https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/OPTIONS
- 浏览器发起的预检请求 - 为了防止对服务器数据产生副作用的请求方法，浏览器会用OPTIONS方法发起一个预检请求，获知服务器是否允许这个跨域请求，允许就发送真实请求，不允许，则阻止真实请求；
- Method: OPTIONS
```
* It uses methods other than GET, HEAD or POST. Also, if POST is used to send request data with a Content-Type other than application/x-www-form-urlencoded, multipart/form-data, ortext/plain, e.g. if the POST request sends an XML payload to the server using application/xmlor text/xml, then the request is preflighted.
* It sets custom headers in the request (e.g. the request uses a header such as X-PINGOTHER)

```