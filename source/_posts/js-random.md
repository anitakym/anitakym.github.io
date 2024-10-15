---
title: js-random
date: 2024-10-12 14:13:14
tags:
---
Object.freeze 是 JavaScript 中的一个内置方法，用于冻结对象。冻结的对象不能被修改（即不能添加或删除属性，不能更改属性值，也不能更改对象的原型）。在你的代码中，Object.freeze 的作用是确保 PUPPETEER_REVISIONS 对象一旦定义，就不再允许进行修改。

具体解释
定义常量:

javascript
export const PUPPETEER_REVISIONS = Object.freeze({
  chrome: '129.0.6668.91',
  'chrome-headless-shell': '129.0.6668.91',
  firefox: 'stable_131.0.2',
});
这里的 PUPPETEER_REVISIONS 是一个冻结的对象。

冻结的影响:

你不能向 PUPPETEER_REVISIONS 添加新的属性。
你不能删除已有的属性。
你不能修改已有属性的值。
你不能更改对象的原型。
例如：

javascript
PUPPETEER_REVISIONS.chrome = '130.0.0';  // 无效操作，抛出错误或忽略更改（严格模式下会抛出错误）
delete PUPPETEER_REVISIONS.firefox;     // 无效操作，不能删除属性
PUPPETEER_REVISIONS.newProperty = 'value';  // 无效操作，不能添加新属性
注意
在你的代码中定义了两个 firefox 键，这样会导致前一个 firefox: 'stable_131.0' 被后一个 firefox: 'stable_131.0.2' 覆盖。因此，最终的 PUPPETEER_REVISIONS 对象中只有一个 firefox 键，值为 'stable_131.0.2'。

修改后的代码
如果你的预期是每个键都有对应唯一的值，可以考虑去掉重复键，或者根据实际情况调整定义。

javascript
export const PUPPETEER_REVISIONS = Object.freeze({
  chrome: '129.0.6668.91',
  'chrome-headless-shell': '129.0.6668.91',
  firefox: 'stable_131.0.2', // 保留最新的值或自己修改
});
确保对象不被更改的场景
Object.freeze 非常适合用于定义常量对象，确保对象及其属性的值在程序运行过程中不被修改。例如：

配置项定义
常量定义（如你的 PUPPETEER_REVISIONS）
防止无意间对重要数据结构的修改
例子
以下是示例，展示 Object.freeze 的使用：

javascript
const CONFIG = Object.freeze({
  apiUrl: 'https://api.example.com',
  timeout: 5000,
});// 试图修改冻结对象将不会生效:
CONFIG.apiUrl = 'https://api.anotherdomain.com'; // 无效
CONFIG.newProp = 'new value'; // 无效

console.log(CONFIG);
// 输出: { apiUrl: 'https://api.example.com', timeout: 5000 }
