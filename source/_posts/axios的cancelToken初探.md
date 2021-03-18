---
title: axios的cancelToken初探
date: 2020-12-29 16:15:50
tags:
      - XMLHttpRequest
---

### axios官方文件源
官方指南：https://github.com/tc39/proposal-cancelable-promises（但是：This proposal has been withdrawn）
代码实现
```
'use strict';

var Cancel = require('./Cancel');

/**
 * A `CancelToken` is an object that can be used to request cancellation of an operation.
 *
 * @class
 * @param {Function} executor The executor function.
 */
function CancelToken(executor) {
  if (typeof executor !== 'function') {
    throw new TypeError('executor must be a function.');
  }

  var resolvePromise;
  this.promise = new Promise(function promiseExecutor(resolve) {
    resolvePromise = resolve;
  });

  var token = this;
  executor(function cancel(message) {
    if (token.reason) {
      // Cancellation has already been requested
      return;
    }

    token.reason = new Cancel(message);
    resolvePromise(token.reason);
  });
}

/**
 * Throws a `Cancel` if cancellation has been requested.
 */
CancelToken.prototype.throwIfRequested = function throwIfRequested() {
  if (this.reason) {
    throw this.reason;
  }
};

/**
 * Returns an object that contains a new `CancelToken` and a function that, when called,
 * cancels the `CancelToken`.
 */
CancelToken.source = function source() {
  var cancel;
  var token = new CancelToken(function executor(c) {
    cancel = c;
  });
  return {
    token: token,
    cancel: cancel
  };
};

module.exports = CancelToken;

```

### XMLHttpRequest
同步请求：原理是 XMLHttpRequest 这个可以传第三个参数，但是不建议用同步请求，会把 JS 执行线程卡住


### Fetch
AbortController
> AbortController接口表示一个控制器对象，允许你根据需要中止一个或多个 Web请求。

文档指南：
https://developer.mozilla.org/zh-CN/docs/Web/API/AbortController

redaxios(Axios has a great API that developers love. Redaxios provides that API in 800 bytes, using native fetch().)
```
// redaxios(https://github.com/developit/redaxios)中，用AbortController实现的CancelToken
/**
	 * @public
	 * @type {AbortController}
	 */
	redaxios.CancelToken = /** @type {any} */ (typeof AbortController == 'function' ? AbortController : Object);

```