---
title: electron应用签名问题
date: 2021-03-08 13:54:39
tags:
---
### 代码签名：
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
无法打开“XXXPro”，因为Apple无法检查其是否包含恶意软件。

已阻止使用“XXXPro”,因为来自身份不明的开发者 仍要打开 


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
- https://kilianvalkhof.com/2019/electron/notarizing-your-electron-application/
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

## 杀毒软件误杀问题处理

### 360（Win）

- 开启360，第一次安装或更新的软件的时候，360会弹出“有程序试图修改关键程序DLL文件”的警告
- 用公司账号登录360软件开放平台。选择首页的提交软件检测并填写相关信息，等待审核。审核通过后解决（在第一次更新时360还是会弹窗，后续每次更新客户端时，在打包后都需执行上述过程，则不会再次弹窗）


### McAfee(Win)
- McAfee 我们当时遇到的问题是，集团给员工配置的电脑，会安装McAfee ，程序会McAfee 被删除。
- 目前解决方案：
1. 如果时集团配备的电脑自带的McAfee 软件，问题已解决，可以通过集团统一配置白名单，放行内部软件;
2. 如果自己装的McAfee 软件，则有关闭实时扫描的权限，可以关闭实时扫描，避免误杀；
- 集团那边收到的信息是，软件触发了自适应威胁防护清理，因为软件的信誉低于配置的清理阈值；
- McAfee 关于误杀的问题，需要我们这边提供软件的英文操作说明，然后进行审核；
- 厂商给的文档里面是让提高软件信誉度（在TIE服务器或McAfee GTI上的信誉值）
- 安全部门给到开发部门的紧急解决流程
```
- 提供一个登录账号用于人工排查
- 先人工安装排查一下是否有异常进程，并用其他杀毒软件交叉验证，尽快反馈结果
- 同时请将问题反馈给Mcafee厂商，判断是否是误报或是如何判断为木马的，以便产品开发进行修改。
- 如果人工排查结果没有发现异常，可以先开启白名单，避免影响业务人员的工作。同时跟进Mcafee的反馈。
```
- 软件如果嵌入网页，尽量https，http请求很容易被判定为高风险
- 我们这边本地没有部署TIE服务器

#### windows - pfx签名
- https://www.electron.build/code-signing.html
- 按照build的官方文档操作即可
- 因为我们是一个仓库，通过配置参数，打包不同的客户端，使用同一个pfx签名，所以配置到打包配置文件里面
- 在build/xxx/config.js里面加上
```
win: {
    icon: "build/xxx/icon.ico",
    target: [
      {
        target: "nsis",
        arch: [
          "ia32"
        ]
      }
    ],
    // 新增下面
    certificateFile: './codesign.pfx',
    certificatePassword: 'xxxxxxxxxx'
  },

```
有个安全性的问题
一旦Windows进行提权的操作，可能会被误认为有危险性
```
+    "requestedExecutionLevel": "requireAdministrator",
     
     "nsis": {
-    "oneClick": true
+    "oneClick": false,
+    "perMachine": false,
+    "allowToChangeInstallationDirectory": true
   },

```

### 清除缓存功能


## 运维问题
> 沉淀了两份文档，一份给运营一份给开发，还有Windows的一些操作指南
● 先做预判，快速有个问题处理导向
● 一定解决问题，不管通过什么方式
● 注意问题记录，积累经验和话术
### installer intergrity check has failed - 下载包不完整

### 安装进度栏卡死 - 彻底卸载之前文件 - %appdata%

### 系统问题，可以选择兼容性处理，右键属性-兼容性-以兼容模式运行这个程序


### 安装完没有能创建快捷方式 - %appdata% -> 到安装目录，发送桌面快捷方式


### 白屏 - 浏览器能打开里面嵌入到网页 - 确认是网络问题后
- 控制面板 -> internet选项 -> 连接 -> 局域网设置

### win7系统.net Framework版本过低
- 登录Microsoft网站https://dotnet.microsoft.com/download/dotnet-framework，下载.net Framework最新版本（推荐.NET Framework 4.8 (recommended)），安装