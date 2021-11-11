---
title: nodejsWeb应用开发-精读
date: 2021-06-10 11:04:07
tags:
---
## Koa:
项目地址：
https://github.com/koajs/koa

一定要拉代码具体看，很适合看源码

### Koa-源码
#### Object.create() 
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/create
```
// v1.x v2.x都使用了这种方式
const response = require('./response');
const context = require('./context');
const request = require('./request');
  this.context = Object.create(context);
  this.request = Object.create(request);
  this.response = Object.create(response);
```
- JavaScript高级程序设计（第4版）_ 原型式继承
```
// 警告 Object.setPrototypeOf()可能会严重影响代码性能。
// Mozilla文档说得很清楚：“在所有浏览器和JavaScript引擎中，修改继承关系的影响都是微妙且深远的。这种影响并不仅是执行Object.setPrototypeOf()语句那么简单，而是会涉及所有访问了那些修改过[[Prototype]]的对象的代码。”
// 为避免使用Object.setPrototypeOf()可能造成的性能下降，可以通过Object.create()来创建一个新对象，同时为其指定原型
let biped = {
  numLegs: 2
}
let person = Object.create(biped)
person.name = 'Matt'
console.log(person.name) // Matt
console.log(person.numLegs) // 2
console.log(person.getPrototypeOf(person) === biped) // true
// ECMAScript 5通过增加Object.create()方法将原型式继承的概念规范化了。这个方法接收两个参数：作为新对象原型的对象，以及给新对象定义额外属性的对象（第二个可选）。在只有一个参数时，Object.create()与这里的object()方法效果相同
// 原型式继承非常适合不需要单独创建构造函数，但仍然需要在对象间共享信息的场合。但要记住，属性中包含的引用值始终会在相关对象间共享，跟使用原型模式是一样的。
```

#### inspect
```
// util.inspect.custom support for node 6+
    /* istanbul ignore else */
    if (util.inspect.custom) {
      this[util.inspect.custom] = this.inspect;
    }
```

```
// 看下node源码 v16.3.0 lib/internal/util/inspect.js
/**
 * Echos the value of any input. Tries to print the value out
 * in the best way possible given the different types.
 *
 * @param {any} value The value to print out.
 * @param {Object} opts Optional options object that alters the output.
 */
/* Legacy: value, showHidden, depth, colors */
function inspect(value, opts) { ... }
inspect.custom = customInspectSymbol;

```

#### nodemon
基本介绍：nodemon用来监视node.js应用程序中的任何更改并自动重启服务
- https://github.com/remy/nodemon
nodemon is a tool that helps develop node.js based applications by automatically restarting the node application when file changes in the directory are detected.
```
"dev": "./node_modules/.bin/nodemon bin/www",
"prd": "pm2 start bin/www",
```
开发阶段，依赖于nodemon监测代码变动，自动重启node.js应用；
生产环境，通过pm2，cluster模式，按cpu核数启动对应进程数（The cluster mode allows networked Node.js applications (http(s)/tcp/udp server) to be scaled across all CPUs available, without any code modifications.）
The cluster module allows easy creation of child processes that all share server ports.
#### koa-views
```
  "dependencies": {
    "consolidate": "0.15.1",
    "debug": "^4.1.0",
    "get-paths": "0.0.7",
    "koa-send": "^5.0.0",
    "mz": "^2.4.0",
    "pretty": "^2.0.0"
  }
```


#### bin/www
```
var server = http.createServer(app.callback());
// app.js
module.exports = app
```

#### app.js
```
// error handler
// middlewares
bodyparser | json | logger | koa-static | koa-views
koa-static _ Koa static file serving middleware, wrapper for [`koa-send`](https://github.com/koajs/send).
// logger
// routes
// error-handling
```
#### koa-static
```
app.use(require('koa-static')(__dirname + '/public'))
```
如上，全局使用的
tips:
static中间件如果放到全局，就会对于每个请求判断一次是不是静态资源，影响QPS；
1.结合koa-mount使用(Mount `koa-static` to a specific path)
2.结合koa-router，按需挂载
```
router.get('/public/*, async (ctx, next) => {
  ctx.url = path.basename(ctx.url)
  await next()
}, static(resolve('./public'), {gzip:true}))
```
#### 模版编译
本身是耗时的，koa-views依赖consolidate提供缓存
```
// consolidate.js _ Template engine consolidation library.
// koa-views
function viewsMiddleware(
  path,
  { autoRender = true, engineSource = consolidate, extension = 'html', options = {}, map } = {}
) ...
const render = engineSource[engineName]

// 支持40多个，可以修改extensions
app.use(views(__dirname + '/views', {
  extension: 'pug'
}))
```
#### 路由routes
```
// routes
app.use(index.routes(), index.allowedMethods())
app.use(users.routes(), users.allowedMethods())
```
没有指定请求路径
```
// koa lib/application.js use 的实现
  /**
   * Use the given middleware `fn`.
   *
   * Old-style middleware will be converted.
   *
   * @param {Function} fn
   * @return {Application} self
   * @api public
   */

  use(fn) {
    if (typeof fn !== 'function') throw new TypeError('middleware must be a function!');
    if (isGeneratorFunction(fn)) {
      deprecate('Support for generators will be removed in v3. ' +
                'See the documentation for examples of how to convert old middleware ' +
                'https://github.com/koajs/koa/blob/master/docs/migration.md');
      fn = convert(fn);
    }
    debug('use %s', fn._name || fn.name || '-');
    this.middleware.push(fn);
    return this;
  }
```
```
  "dependencies": {
    "debug": "^3.1.0",
    "http-errors": "^1.3.1",
    "koa-compose": "^3.0.0",
    "methods": "^1.0.1",
    "path-to-regexp": "^1.1.1",
    "urijs": "^1.19.0"
  },
  // path-to-regexp > Turn an Express-style path string such as `/user/:name` into a regular expression.
  // 正则路由匹配模块 - 复杂且效率较高
  // go / fastify(https://github.com/fastify/fastify) - find-my-way 基于基数树radix tree实现
  // fastify
  "requires": {
        "@fastify/ajv-compiler": "^1.0.0",
        "abstract-logging": "^2.0.0",
        "avvio": "^7.1.2",
        "fast-json-stringify": "^2.5.2",
        "fastify-error": "^0.3.0",
        "fastify-warning": "^0.2.0",
        "find-my-way": "^4.0.0",
        "flatstr": "^1.0.12",
        "light-my-request": "^4.2.0",
        "pino": "^6.2.1",
        "proxy-addr": "^2.0.7",
        "readable-stream": "^3.4.0",
        "rfdc": "^1.1.4",
        "secure-json-parse": "^2.0.0",
        "semver": "^7.3.2",
        "tiny-lru": "^7.0.0"
      }
    // find-my-way
    A crazy fast HTTP router, internally uses an highly performant [Radix Tree](https://en.wikipedia.org/wiki/Radix_tree) (aka compact [Prefix Tree](https://en.wikipedia.org/wiki/Trie)), supports route params, wildcards, and it's framework independent.

    If you want to see a benchmark comparison with the most commonly used routers, see [here](https://github.com/delvedor/router-benchmark).<br>
    Do you need a real-world example that uses this router? Check out [Fastify](https://github.com/fastify/fastify) or [Restify](https://github.com/restify/node-restify).
```
trek-router的基准测试

#### debug
```
// 增加配置，针对这个项目 /bin/www
    {
      "type": "node",
      "request": "launch",
      "name": "Launch Program",
      "program": "${workspaceRoot}/bin/www",
    }
// 启动调试
// 打断点
// 浏览器发起请求 127.0.0.1:3000 触发断点
```

### 框架演进
koa && connect 只提供中间件内核，不内置中间件
express 绑定了必要的基础插件
#### http
#### connect（“编程时会区分可变状态和不可变状态，可变的抽取出去，不可变的固化下来。Connect提供了可变部分的插件化，对于Node.js Web应用开发来说，这是演进中必要的一步。” ）
得考虑中间件的执行顺序
#### express
app.listen()
server.listen()
#### koa
koa-router | koa-trie-router(快速检索多叉树)

### 测试
```
ava
+
supertest => express 里经典测http api框架
```
-w 支持监控文件变动测试
```
    "test": "./node_modules/.bin/ava -v -w"
```
原子性测试:
因为是ava是并行执行的，如果不加-s参数的话，所以要注意保证原子性

```
常用模块
chai 
sinon
zombie
cucumber-js
nightwatch
```

## 中间件

## 框架介绍
- https://eggjs.org/zh-cn/intro/index.html
- 可以看看egg的设计原则