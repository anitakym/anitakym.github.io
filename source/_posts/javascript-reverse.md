---
title: javascript-reverse
date: 2021-03-16 15:32:13
tags:
---
## reverse
文档指南：https://www.freecodecamp.org/news/how-to-reverse-a-string-in-javascript-in-3-different-ways-75e4763c68cb/



## for ... in
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in
- Reference - Statements&declarations
- for ... in 不应用于迭代一个数组，因为迭代的顺序是依赖于执行环境的
- 如果需要迭代访问顺序很重要的数组，用整数索引去进行for 的循环
- for in 适用于debug
- 具体可以看MDN的文档

## callback

## 立即执行函数
```
    const width = 512
      const height = 512
      ;(async function () {
        const program = await doodle.load('./lib/fragment.glsl')
        doodle.useProgram(program)
        doodle.uniforms.resolution = [width, height]
        doodle.render()
      })()
```
- ; 如果少了，就会报错
- `{(intermediate value)(intermediate value)} is not a function`
- 立即执行函数前面需要分号


#### ReferenceError
- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/ReferenceError
- 报错合集:The ReferenceError object represents an error when a non-existent variable is referenced.
- 当一个不存在的变量被引用时发生的错误
```
function foo () {
  console.log(bar)
  let bar = 3
}
foo()
```