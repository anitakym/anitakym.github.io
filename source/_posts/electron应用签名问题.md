---
title: electron应用签名问题
date: 2021-03-08 13:54:39
tags:
---
代码签名：
- 自定义测试（无法自动更新）签名：
1. 钥匙串访问=>证书助理=>创建证书=>自定签名的根证书，代码签名
2. export CSC_NAME="Electron Auto Update"
（https://www.electron.build/code-signing）
<pre>
macOS and Windows code signing is supported. Windows is dual code-signed (SHA1 & SHA256 hashing algorithms).

On a macOS development machine, a valid and appropriate identity from your keychain will be automatically used.

CSC_NAME	macOS-only Name of certificate (to retrieve from login.keychain). Useful on a development machine (not on CI) if you have several identities (otherwise don’t specify it).
</pre>

- 从Xcode里面 偏好设置-accounts-manage certificates +developer id application ,加到钥匙串里面即可

### 包签名
无法打开“互动课堂Pro”，因为Apple无法检查其是否包含恶意软件。

已阻止使用“互动课堂Pro”,因为来自身份不明的开发者 仍要打开 


### 自定义安装界面
https://www.electron.build/configuration/dmg
可以在electron-builder的configuration里面进行配置：
macOS我们目前是dmg的产出，可以按照文档进行配置

### 创建目录路径选择
根目录：/
用户目录：～
在根目录创建文件的时候会出现：read-only file system



### 查看日志
cd ~/Library/Cache
cd ~/Library/Application Support

cd ~/Library/Logs

### 公证
现有软件，已用集团账号导出的证书进行了code signing —— 代码的开发者签名10.14

https://support.apple.com/zh-cn/guide/mac-help/mh40616/mac 
（给用户看的操作链接）

https://support.apple.com/zh-cn/HT202491
（高版本的系统还需要公证） Catalina 及以上版本

2019的wwdc19 公证面面观
公证就是关于在分发前识别和拦截恶意的Mac软件，而无需App Review团队或Mac App Store的参与。在去年推出。
公证方法：
https://oldj.net/article/2019/12/29/electron-builder-sign-and-notarize-for-macos/

https://github.com/electron/electron-notarize

```
// 公证操作执行命令：
xcrun altool --notarize-app --primary-bundle-id "cn.xxx.xx.xxxx" --username "xxx@xxx.cn" --password "apppasswd" --asc-provider "providerNameXXX" -t osx --file xxx.dmg
// 说明：
// xxx.dmg 替换为要公证的文件名，执行命令和要公证的文件包（xxx.dmg）在同一目录下
// cn.xxx.xx.xxxx 替换成应用到bundleid
// providerNameXXX 是providerName，根据邮箱和密码查出来的
xcrun altool --list-providers --username "xxx@xxx.cn" --password "apppasswd"
// 结果如下，则上传成功：
No errors uploading 'xxx.dmg'.
RequestUUID = "一串字符串"
// 公证成功会收到邮件：
// 或者可以通过命令查公证状态：
xcrun altool --notarization-info "RequestUUID" --username "xxx@xxx.cn" --password "apppasswd"
公证成功后，安装APP，不会再有安全提示拦截（每次上线新版本前需进行公证）

```