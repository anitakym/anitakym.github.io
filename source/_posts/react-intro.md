---
title: react-intro
date: 2021-04-15 13:30:33
tags:
---
- 参考文档：
https://btholt.github.io/complete-intro-to-react-v5/intro


### creat-react-app
https://github.com/facebook/create-react-app/issues/10161
关于eslintcache文件产生的位置问题(4.0.1)

eslint --cache false可以本地起效，但是不是解决方案

move .eslintcache into node_modules/.cache
https://github.com/facebook/create-react-app/pull/10346
react team 的哥们回复
https://github.com/facebook/create-react-app/pull/9977



eslint: {
    cache: false,
  },

4.0.2


to ignore a file already tracked you also need to run git rm --cached .eslintcache
gitignore


### 修改PORT，HOST
直接
.env
PORT = 3003
HOST = '127.0.0.1'

