---
title: 谈一谈package-json文件
date: 2020-10-22 11:06:19
tags:

---

> 官方文档指南：https://docs.npmjs.com/files/package.json

### version 
- semver - 见```软件版本```博文
### main 属性
- 项目入口 （被import｜require，默认入口main指定）
- 如果不填的话，默认是找文件夹根目录下的index
<pre>
The main field is a module ID that is the primary entry point to your program. That is, if your package is named foo, and a user installs it, and then does require("foo"), then your main module’s exports object will be returned.

This should be a module ID relative to the root of your package folder.

For most modules, it makes the most sense to have a main script and often not much else.
</pre>

### scripts
- 带有命令行的node模块，不需要全局安装，scripts中定义的脚本根据node_modules找到对应模块并启动脚本指令

### keywords | author | license
### TIPS
#### 中文字符
- Package.json 里面不要出现中文，不然会出现解析错误
-项目标题不要大写字母，要全小写