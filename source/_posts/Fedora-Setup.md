---
title: Fedora-Setup
date: 2022-07-14 14:06:05
tags:
---
### dev
- vscode
- chrome



### basic
#### VPN
- clashy - appimage客户端有点问题（）

#### shortCut
- 基本的复制粘贴 - 保证和Mac体验接近
#### 远程控制
- teamviewer - 有官方支持的版本 - https://www.teamviewer.cn/

### 目前有问题的软件
- 百度云盘 - 官方提供的rpm包不可用

### Documents
- https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/Preface/


### network
```
client:
tar xzvf xxx-x64-linux.tar.gz
cd xxx-x64-linux
./xxx(abbr)

if clash
profiles 
download from a url
allow LAN
system proxy
start with linux

system:
network proxy
manual

http proxy LAN xxxx(port)
https proxy LAN xxxx(port)
```

### keymapping
- 哈哈，这个很重要，能避免mac和fedora使用时候，ctrl和cmd键的人工大脑切换，提高效率，降低切换成本
- sudo dnf install gnome-tweaks
- tweaks - Additional layout options - alt and win behavior - ctrl is mapped to win and the usual ctrl
- 然后如果是想要控制别的，就可以使用系统提供的快捷键配置
### wayland


### 字体显示问题
- 先是系统语言设置为了英文，这种情况下的中文渲染不是简体字，切换为中文系统语言，保留之前英文的文件夹命名

#### rpm
- https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/RPM/

#### wayland
- https://docs.fedoraproject.org/en-US/fedora/latest/system-administrators-guide/Wayland/
