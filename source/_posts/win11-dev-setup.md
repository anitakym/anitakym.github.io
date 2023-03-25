---
title: win11-dev-setup
date: 2022-11-29 14:57:32
tags:
---
#### 软件安装管理
- https://github.com/chocolatey/choco

#### 快捷键处理

- https://www.autohotkey.com/ - 按指导下载安装autohotkey
- 
```
# 具体脚本配置参考这篇
https://blog.csdn.net/weixin_44839047/article/details/126166602
```
- 右键脚本，更多选项，compile，这样就可以生成一个.exe的可执行文件
- 把这个可执行文件放在开机自动启动的地方（%USERPROFILE%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup）

#### vscode
```
在 ESLint 中，"Delete cr (Carriage Return) eslint" 是一个规则，它用于检测代码中是否包含了 Windows 风格的行尾符（即 Carriage Return + Line Feed，或者简写为 CRLF）。

由于不同操作系统使用不同的行尾符，因此在不同操作系统之间共享代码时，可能会出现类似“missing newline at end of file”的问题。这个规则就是用来解决这个问题的。

当启用 "Delete cr (Carriage Return)" 规则时，ESLint 将会检测代码中是否包含了 Windows 风格的行尾符，并将其替换为 Unix 风格的行尾符（即 Line Feed，简写为 LF），从而消除跨平台共享代码时遇到的行尾符问题。

例如，在以下代码中：

function add(a, b) {
  return a + b;
}
如果该文件使用的是 Windows 风格的行尾符，则该文件的结尾将会有一个 Carriage Return 字符，这可能会导致 ESLint 报告 "missing newline at end of file" 错误。启用 "Delete cr (Carriage Return)" 规则后，ESLint 将自动删除该字符并将其替换为 LF 字符，以消除这个错误。

需要注意的是，如果您想在语法上保留 Windows 风格的行尾符，请勿启用 "Delete cr (Carriage Return)" 规则，或者调整相关配置，以便在特定情况下忽略或禁用该规则。

warning: in the working copy of 'src/app.controller.spec.ts', LF will be replaced by CRLF the next time Git touches it
这个警告信息是 Git 在 Windows 系统上的表现，它提示您在 Git 操作过程中可能会修改文件的行尾符格式。

具体来说，该警告表示您的 Git 工作副本中包含了使用 Unix 风格的行尾符（即 LF 字符），但是当 Git 在 Windows 平台上操作该文件时，它将自动替换为 Windows 风格的行尾符（即 CRLF 字符）。这可能会导致一些问题，例如代码格式化和跨平台共享代码等问题。

为了避免这个问题，可以在 Git 配置中设置 core.autocrlf 属性。如果您希望在提交代码时将其转换为 Windows 风格的行尾符，则可以将此属性设置为 true；如果您希望保留原始的行尾符格式，则可以将此属性设置为 false；如果您希望在 Windows 平台上自动转换为 CRLF 行尾符，并在其他平台上保留原始格式，则可以将此属性设置为 input。

例如，要将 core.autocrlf 设置为 true，可以执行以下命令：

git config --global core.autocrlf true
这将告诉 Git 在提交代码时将所有行尾符都转换为 CRLF 格式。

需要注意的是，行尾符格式的问题可能会对代码的版本管理和跨平台共享造成影响，请谨慎处理并选择适合您的项目和团队的最佳实践。

在 Windows 中，您可以使用多种方法修改文件的行尾符类型，以便与 Unix/Linux 或 macOS 上的文件相兼容。下面是一些常见的修改行尾符的方法：

使用文本编辑器：大多数文本编辑器都支持设置行尾符类型。例如，在 Visual Studio Code 中，您可以单击底部状态栏中的 CRLF 按钮，以切换行尾符类型。选择 LF 将使其更改为 Unix 风格的行尾符，而选择 CR 和 CRLF 则将其更改为 Macintosh 和 Windows 风格的行尾符。

使用 Git 命令：如果您正在使用 Git 进行版本控制，则可以使用以下命令将所有文件的行尾符转换为 LF（Unix 风格）：

git config --global core.autocrlf input
git rm --cached -r .
git reset --hard
这将配置 Git 在提交代码时自动将行尾符转换为 LF，并将所有文件的缓存清除并重新检出。

使用 PowerShell 脚本：您可以编写一个 PowerShell 脚本来递归地遍历目录并将所有文件的行尾符转换为 LF，如下所示：
Get-ChildItem -Recurse | Where-Object {-not $_.PSIsContainer} | ForEach-Object {
  (Get-Content $_.FullName) | Set-Content $_.FullName -Encoding UTF8
}
此脚本将读取所有文件的内容并将其写入同一文件中，但同时将行尾符转换为 LF。

需要注意的是，修改行尾符可能会影响代码在其他操作系统上的兼容性，因此请谨慎操作并确保您了解相关风险和最佳实践。
```