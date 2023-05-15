---
title: nodejs-path
date: 2021-03-04 12:12:00
tags:
    - node
---
### 文档指北：
https://nodejs.org/api/path.html#path_path
http://nodejs.cn/api/path.html
还是推荐dash,可以快速搜索，然后选择右上角copy online page

### 项目经验
node服务项目







electron项目

### glob
- https://www.npmjs.com/package/glob
- https://github.com/isaacs/node-glob
- 支持配置通配符规则的方式来扫描文件目录，像在 shell 里执行命令一样，获取匹配对应规则的文件
```
__dirname 脚本文件所在目录
process.cwd() 脚本文件执行目录
```

### 当前文件和目录所在位置
- __dirname __filename  (express-generator __dirname确定项目模版目录所在位置)

### 当前终端执行路径
- process.cwd()

### 当前系统用户主目录
- process.env.HOME - HOMEPATH - USERPROFILE
- os - homedir


#### 模块依赖图
- brew install graphviz
- npm i -g npm2dot