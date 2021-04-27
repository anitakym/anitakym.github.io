---
title: MacOS使用Tips
date: 2020-04-06 16:35:36
tags:
    - MacOS
---
> 写在开头：macOS是基于BSD Unix的，所以很多命令和Linux有细微的差别，如（ps, ls, tail, awk, sed）,比如我们```man ps```,会显示：BSD General Commands Manual。如果我们写跨平台的bash脚本的时候，需要注意一些命令，仔细的做好测试

#### 查看版本信息
sw_vers

#### pbcopy/pbpaste
```
ls ~ | pbcopy
pbcopy < test.txt
curl xxx | pbcopy
pbpaste >> test.txt
```

#### mdfind 对标spotlight
```
mdfind -onlyin ~/Documents xxx
```
#### mdls  list metadata (such as photo EXIF info)


#### 命令行中打开finder
```open .```
//打开应用
```open -a /Applications/Whatever.app```

#### 文件名大小写区分
windows 和 mac
系统里面文件名不区分大小写


Linux里面则会区分大小写

case-sensitive-paths-webpack-plugin

https://www.npmjs.com/package/case-sensitive-paths-webpack-plugin


#### brew
brew -ls

#### screencapture
cmd+shift+3/4
```screencapture --help```

#### 关闭mac输入法首字母大写

系统偏好设置
键盘
文本

去掉首字母大写的即可

#### 查找系统安装字体
brew install fontconfig
fc-list :zang-zh
fc-list : file family | grep \/Library

搜索：字体册
Font Book.app

#### 推荐app
翻译类：
Google DeepL translator
极光词典（Mac和IOS都可以使用）
工具类：
magnet（https://magnet.crowdcafe.com/?utm_source=help）—— 分窗口软件
shadowsocks
charles（抓包）
dash（查文档）
vscode（代码编辑）
Alfred（全局搜索）
SwitchHosts（host配置）
Notability（笔记）
命令行：
pandoc（文件格式转换）

