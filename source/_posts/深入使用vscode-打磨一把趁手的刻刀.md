---
title: 深入使用vscode-打磨一把趁手的刻刀
date: 2021-03-08 11:01:58
tags:
---
### 参考资源：
gitbook （https://burkeholland.gitbook.io/vs-code-can-do-that/）
系统的介绍了vscode的使用，还有一些很棒的tricks，各种拓展的选择和使用

frontend masters 有 course，gitbook里面是exercise

如果使用上面的材料：
vscode可以安装这个extension ——
https://marketplace.visualstudio.com/items?itemName=burkeholland.vs-code-can-do-that
docker ——
https://docs.docker.com/get-docker/
git + node



### 重要的快捷键
- 快捷用vscode打开项目
```
code .
```
需要先：
(Cmd/Ctrl + Shift + P) and select "Shell Command: Install 'code' command in path".

Mac的话，也可以构建任务流，这样就可以右键选择，里面“用vscode打开了”

- Mac里面Cmd是主要的控制键，Windows里面Ctrl是主要的控制键
- 一些常用的快捷键(写成Mac的，Windows的换控制键为Ctrl即可)
  - sidebar 的切换(Cmd + B) 
  - 打开命令面板(Cmd + shift + P)
  - 打开文件面板(Cmd + P)
  - 打开设置(Cmd + ,)
  - 集成终端视图切换(Ctrl + `) => (私人换了，一般应该是Cmd + `)

### 定制编辑器

#### 切换主题/安装icon主题/切换字体
(Cmd/Ctrl + Shift + P)

- "Preferences: Color Theme".
拖到最底下，可以下载想要安装的主题（颜色主题）

- "Preferences: File Icon Theme"
material 比较清晰，可以区分workspace和file(icon主题)

- FiraCode/Hasklig/Monoid
  - https://github.com/tonsky/FiraCode
  - https://github.com/i-tu/Hasklig

- font ligatures
  - 有些字体支持 "字体连字"。这些符号代表我们在编程中使用的复合符号。如果你正在使用的字体支持它们，你可以通过勾选 "Editor.Font Ligatures"框来打开它们。

