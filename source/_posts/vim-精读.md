---
title: vim-精读
date: 2021-06-22 16:42:57
tags:
---
### 参考文档
https://yianwillis.github.io/vimcdoc/doc/help.html

> 设计理念 - 模式的转换 + 命令的组合 + 丰富的插件 ； 向后兼容较好； Bram Mooleanaar; Vi Imitation -> Vi IMproved; Bill Joy
## 平时遇到的问题
### swap file
按提示做选择即可

## basic - concept - command
- normal模式 （ESC回到这个，命令在这个模式下输入）
- insert模式 (insert - i |  append - a 可进入)
- visual模式 (选择文本块 v)
- command-line模式（: | /-搜索 | ?-搜索）



#### tips
- 如果用的远程终端软件 - 记得设置远程字符集为UTF-8
- mac - which vim
- mac - MacVim - 图形化界面 - homebrew
- 启动中文教程 - LANG=zh_CN.UTF-8 vimtutor


### Janus - 集成套件
`curl -Lo- https://bit.ly/janus-bootstrap | bash`
- ack.vim
- ctrlp
- nerdtree
- supertab