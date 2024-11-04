---
title: llms-reverse-js
date: 2024-11-01 16:12:10
tags:
---
- https://thejunkland.com/blog/using-llms-to-reverse-javascript-minification
- https://github.com/jehna/humanify
- https://github.com/jamiebuilds/babel-handbook/blob/master/translations/en/plugin-handbook.md
- https://www.npmjs.com/package/babel-plugin-transform-beautifier
- https://www.npmjs.com/package/debundle


- LLMs 真正擅长的另一个任务是摘要，这几乎就是我们在第3步中所做的。唯一的专业化要求是输出需要足够简短，并格式化为驼峰式大小写。
- 有方法可以控制 LLM 的输出，如 guidance 和 outlines。这些工具使用不同的技术确保 LLM 的输出符合期望的格式。
- 使用传统工具（如 Babel）在其作用域内重命名 Javascript 变量是一个已解决的问题。Babel 首先将代码解析成一个抽象语法树（AST，代码的机器表示形式），这很容易使用行为良好的算法进行修改。

- https://guidance.readthedocs.io/
- https://github.com/dottxt-ai/outlines
使用 webcrack 解包 webpack 包
通过 transform-beautifier 和一些自定义的 Babel 插件运行代码，这些插件可以逆转无损压缩
遍历代码中的所有变量，请求 LLM 描述其意图并根据该描述生成更好的名称
使用 Babel 重命名变量
进行最后一轮的 Prettier 以确保优美的空格
