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
brew - 下载不带界面的命令行的工具和第三方库
brew cask - 下载带界面的应用软件
brew install curl
brew cask install chrome 

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
Google DeepL translator - https://www.deepl.com/app/thanks
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
#### 方法
> 因为想把有道云笔记迁移到notability上，但是有道云笔记只支持在PC客户端进行全部导出到操作，所以需要从PC快速分享文件到Mac上

首先保证windows电脑和Mac 在同一局域网
- window上： 运行-> cmd -> ifconfig -> 得到本机在局域网到ip
- window上： 右键文件夹-> 属性 ->共享-> 高级 -> 共享此文件夹 -> 确定
- Mac 上: 在 Finder 到前往里面选择’连接服务器’, 输入 smb://10.200.170.52（你获得的windows电脑的ip）,点连接， 然后输入windows的管理员的名称和密码即可（在windows的设置->账户信息里面可以查到）。


## windows - 公司无线edu
- 网络和共享中心-设置新的连接和网络-手动连接到无线网络
- 网络名一定得为EDU，不然搜索不到
- 网络名-EDU + 安全类型-WPA2-企业 —— 加密类型AES
- 下一步 - 更改连接设置
- 安全 - 设置 - 取消掉通过高验证证书来验证服务器的身份｜ 取消自动用Windows的账号登录
- 安全 - 高级设置 - 802.1X设置 - 选择“指定身份验证模式（P）”
```
https://baike.baidu.com/item/WPA2/4913331
WPA2 = IEEE 802.11i = IEEE 802.1X/EAP + WEP(选择性项目)/TKIP/CCMP

大多数企业和许多新的住宅 Wi-Fi 产品都支持 WPA2。截止到 2006 年 03 月，WPA2 已经成为一种强制性的标准。WPA2 需要采用高级加密标准 (AES) 的芯片组来支持。
WPA2 有两种风格：WPA2 个人版和 WPA2 企业版。WPA2 企业版需要一台具有 IEEE 802.1X 功能的 RADIUS (远程用户拨号认证系统) 服务器。没有 RADIUS 服务器的 SOHO 用户可以使用 WPA2 个人版，其口令长度为 20 个以上的随机字符，或者使用 McAfee 无线安全或者 Witopia Secure MyWiFi 等托管的 RADIUS 服务。
```