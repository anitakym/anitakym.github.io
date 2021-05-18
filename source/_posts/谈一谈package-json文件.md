---
title: 谈一谈package-json文件
date: 2020-10-22 11:06:19
tags:

---

> 官方文档指南：https://docs.npmjs.com/files/package.json


#### main 属性
如果不填的话，默认是找文件夹根目录下的index
<pre>
The main field is a module ID that is the primary entry point to your program. That is, if your package is named foo, and a user installs it, and then does require("foo"), then your main module’s exports object will be returned.

This should be a module ID relative to the root of your package folder.

For most modules, it makes the most sense to have a main script and often not much else.
</pre>
