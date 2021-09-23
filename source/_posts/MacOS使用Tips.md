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

(vue项目本身，文件和文件夹命名，都是kebab-case的，这样也直接避免了这个问题)

#### brew
brew -ls

#### screencapture
cmd+shift+3/4
（3全屏，4选择器）
cmd+shift+4+Space（窗口）
```screencapture --help```

#### 关闭mac输入法首字母大写

系统偏好设置
键盘
文本

去掉首字母大写的即可

#### 共享目录访问
1.打开finder
2.cmd+K
3.smb://xxxx/xxx

#### 浏览器中打开文件
cmd + O
选择文件即可
#### 查找系统安装字体
brew install fontconfig
fc-list :zang-zh
fc-list : file family | grep \/Library

搜索：字体册
Font Book.app

#### 推荐app
可参考：https://github.com/jaywcjlove/awesome-mac/blob/master/README-zh.md

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
SwitchHosts（host配置）- 或者编辑/etc/hosts文件
Notability（笔记）
命令行：
pandoc（文件格式转换）

#### 文档手写签名
用预览功能：
打开PDF文档后，点击工具=>注解=>签名（管理签名），

#### 隔空投送
- 修改本机名称：系统偏好设置=>共享，修改即可；


#### 快捷键
cmd + M 最小化窗口
cmd + T 新Tab
cmd + W 关闭窗口
cmd + Q 退出程序
cmd + Space 切换输入法
cmd + 拖动非最前面窗口，可以避免拖动导致的激活
cmd + Del 移到废纸篓
ctrl + cmd + Space 输入emoji

#### 活动监视器
activity monitor （spotlight里面搜索）


