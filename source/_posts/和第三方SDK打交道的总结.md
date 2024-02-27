---
title: 和第三方SDK打交道的总结
date: 2024-02-27 14:10:27
tags:
---
在不修改原型链、BOM和DOM对象的情况下，我们可以通过使用帮助函数（helper function）或者通常被称为“wrapper”的方式，对第三方 SDK 打非侵入式的补丁或者说是进行封装。

具体的方法如下：

1. **建立包装函数（Wrapper Function）：** 创建一个新的函数，该函数内部调用第三方 SDK 的相关方法，并额外添加我们需要的功能。例如：

```javascript
// 第三方 SDK 方法
function thirdPartyMethod(a, b) { /* ... */ }

// 包装函数
function wrappedMethod(a, b) {
    // 在调用原有方法前执行新逻辑...
    
    thirdPartyMethod(a, b);
    
    // 在调用原有方法后执行新逻辑...
}
```

这种方式的优势是可以在不触碰原有功能的情况下添加新的功能或行为。

2. **使用代理（Proxy）：** JavaScript的 Proxy 对象可以创建一个对象的代理，从而可以拦截该对象的某些操作。比如你可以拦截对一个对象的函数调用，然后在函数调用前后执行自己的逻辑。

以下是一个使用 Proxy 的示例：

```javascript
let thirdPartyObject = {
    thirdPartyMethod: function(a, b) { /* ... */ }
};

let proxy = new Proxy(thirdPartyObject, {
    get: function(target, prop) {
        if (typeof target[prop] === 'function') {
            return function(...args) {
                // 在调用原有方法前执行新逻辑...
                
                let result = target[prop](...args);
                
                // 在调用原有方法后执行新逻辑...
                
                return result;
            };
        } else {
            return target[prop];
        }
    }
});
```

此时，通过 `proxy.thirdPartyMethod(a, b)` 调用方法，就会执行我们的新逻辑，同时不会更改原有的对象和方法，算是一种非侵入式的补丁方式。

请注意，对于 Proxy 的方式，由于 Proxy 是 ES6 的一个特性，对于不支持 ES6 的环境，这种方式则无法使用。

总体而言，要非侵入式地对第三方 SDK 打补丁，建立一个包装或者代理层是一个比较有效的方式。这种方式可以让我们添加自己的代码逻辑，又不修改或者侵入第三方 SDK 的原有逻辑。

JavaScript的Proxy对象可以通过polyfill来实现。但是这只适用于ES5和以后的版本，因为早期版本的JavaScript并未提供能够完全模拟Proxy对象的功能。

示例代码如下：

```js
if(typeof Proxy !== 'function') {
    Proxy = function(target, handler) {
        //TODO: add logic here 
        return target;
    };
};
```

这只是一个非常简单的示例，真正实现一个完整的Proxy polyfill会非常复杂且困难。在实际应用中，最好的方法可能是检查浏览器是否支持Proxy，并且在不支持的情况下提供备用策略，因为除了某些边缘情况，很难编写出一个与原生Proxy功能完全一致的polyfill。

需要注意的是，由于Proxy对象涉及许多底层操作，不可能完全地在不支持它的JavaScript环境中模拟出来，所以并不存在一个完整且可靠的Proxy polyfill。实际上，最好尽量在支持Proxy的环境中使用它，并且考虑它的可用性和兼容性问题。