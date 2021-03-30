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
