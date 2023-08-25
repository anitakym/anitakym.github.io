---
title: JSX深入理解
date: 2023-02-16 14:19:57
tags:
---
#### search
- 在https://reactjs.org/docs/getting-started.html，搜索JSX
```
- 高级指引
  - 不使用JSX的React - 每个 JSX 元素只是调用 React.createElement(component, props, ...children) 的语法糖。因此，使用 JSX 可以完成的任何事情都可以通过纯 JavaScript 完成。
  - 深入JSX - https://zh-hans.reactjs.org/docs/jsx-in-depth.html#gatsby-focus-wrapper
- 核心概念
  - JSX简介 - https://zh-hans.reactjs.org/docs/introducing-jsx.html - why & how
- FAQ
  - Babel、JSX及构建过程 - https://zh-hans.reactjs.org/docs/faq-build.html
- API Reference
  - React术语词汇表 - JSX

```
- 在https://beta.reactjs.org/，搜索JSX
  - Writing Markup with JSX
  - JavaScript in JSX with Curly Braces


#### 老版本的React中，写JSX文件，默认引入React
- jsx被babel编译后，React.createElement，所以需要引入React，防止找不到React报错


### Fiber
- https://github.com/acdlite/react-fiber-architecture
- Fiber is the new reconciliation engine in React 16. Its main goal is to enable incremental rendering of the virtual DOM.
- 在调和阶段，React element 对象的每一个子节点都会形成一个与之对应的fiber对象，然后通过sibling，return，child将每一个fiber对象联系起来

```
export const FunctionComponent = 0;       // 函数组件
export const ClassComponent = 1;          // 类组件
export const IndeterminateComponent = 2;  // 初始化的时候不知道是函数组件还是类组件 
export const HostRoot = 3;                // Root Fiber 可以理解为根元素 ， 通过reactDom.render()产生的根元素
export const HostPortal = 4;              // 对应  ReactDOM.createPortal 产生的 Portal 
export const HostComponent = 5;           // dom 元素 比如 <div>
export const HostText = 6;                // 文本节点
export const Fragment = 7;                // 对应 <React.Fragment> 
export const Mode = 8;                    // 对应 <React.StrictMode>   
export const ContextConsumer = 9;         // 对应 <Context.Consumer>
export const ContextProvider = 10;        // 对应 <Context.Provider>
export const ForwardRef = 11;             // 对应 React.ForwardRef
export const Profiler = 12;               // 对应 <Profiler/ >
export const SuspenseComponent = 13;      // 对应 <Suspense>
export const MemoComponent = 14;          // 对应 React.memo 返回的组件
```

```
child： 一个由父级 fiber 指向子级 fiber 的指针。
return：一个子级 fiber 指向父级 fiber 的指针。
sibling: 一个 fiber 指向下一个兄弟 fiber 的指针。
```

```
在 jsx 中写的 map 数组结构的子节点，外层会被加上 fragment 
map 返回数组结构，作为 fragment 的子节点
```


### babel
JSX 语法实现来源于这两个 babel 插件：

@babel/plugin-syntax-jsx ： 使用这个插件，能够让 Babel 有效的解析 JSX 语法。
@babel/plugin-transform-react-jsx ：这个插件内部调用了 @babel/plugin-syntax-jsx，可以把 React JSX 转化成 JS 能够识别的 createElement 格式。
#### automatic Runtime
- 新版本 React 已经不需要引入 createElement ，这种模式来源于 Automatic Runtime
```
"presets": [    
    ["@babel/preset-react",{
    "runtime": "automatic"
    }]     
],
```
#### Classic Runtime
- 经典模式下，使用 JSX 的文件需要引入 React ，不然就会报错

#### code
- 可以调用babel API试试编译结果
```
const fs = require('fs')
const babel = require("@babel/core")

/* 第一步：模拟读取文件内容。 */
fs.readFile('./element.js',(e,data)=>{ 
    const code = data.toString('utf-8')
    /* 第二步：转换 jsx 文件 */
    const result = babel.transformSync(code, {
        plugins: ["@babel/plugin-transform-react-jsx"],
    });
    /* 第三步：模拟重新写入内容。 */
    fs.writeFile('./element.js',result.code,function(){})
})

```

- The term "JSX" in React refers to "JavaScript XML". It's a syntax extension for JavaScript, used within React to represent HTML-like components. This combination of JavaScript and XML (HTML-like syntax) allows developers to create their own components or reuse components in a very readable and intuitive way.