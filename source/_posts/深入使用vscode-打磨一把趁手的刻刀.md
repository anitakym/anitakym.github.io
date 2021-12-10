---
title: 深入使用vscode-打磨一把趁手的刻刀
date: 2021-03-08 11:01:58
tags:
---

### 参考资源：

gitbook （https://burkeholland.gitbook.io/vs-code-can-do-that/）
系统的介绍了 vscode 的使用，还有一些很棒的 tricks，各种拓展的选择和使用

frontend masters 有 course，gitbook 里面是 exercise

如果使用上面的材料：
vscode 可以安装这个 extension —— (慎重全部安装，可以查看下，按需安装)
https://marketplace.visualstudio.com/items?itemName=burkeholland.vs-code-can-do-that
docker ——
https://docs.docker.com/get-docker/
git + node

提供了一个测试项目：
git clone https://github.com/burkeholland/workshop-vs-code-can-do-that

### 重要的快捷键

- 快捷用 vscode 打开项目

```
code .
```

需要先：
(Cmd/Ctrl + Shift + P) and select "Shell Command: Install 'code' command in path".

Mac 的话，也可以构建任务流，这样就可以右键选择，里面“用 vscode 打开了”

- Mac 里面 Cmd 是主要的控制键，Windows 里面 Ctrl 是主要的控制键
- 一些常用的快捷键(写成 Mac 的，Windows 的换控制键为 Ctrl 即可)
  - sidebar 的切换(Cmd + B)
  - 打开命令面板(Cmd + shift + P)
  - 打开文件面板(Cmd + P)
  - 打开设置(Cmd + ,)
  - 集成终端视图切换(Ctrl + `) => (私人换了，一般应该是Cmd + `)

### 定制编辑器

#### 切换主题/安装 icon 主题/切换字体

(Cmd/Ctrl + Shift + P)

- "Preferences: Color Theme".
  拖到最底下，可以下载想要安装的主题（颜色主题）

- "Preferences: File Icon Theme"
  material 比较清晰，可以区分 workspace 和 file(icon 主题)

- FiraCode/Hasklig/Monoid

  - https://github.com/tonsky/FiraCode
  - https://github.com/i-tu/Hasklig

- font ligatures
  - 有些字体支持 "字体连字"。这些符号代表我们在编程中使用的复合符号。如果你正在使用的字体支持它们，你可以通过勾选 "Editor.Font Ligatures"框来打开它们。

#### 编辑器调整

- minimap(缩略图),其实不太好用，可以关掉

  - Settings(Cmd+,) => 搜索 Minimap => 取消 enable 的选择

- sidebar 位置调整

  - 在 cmd + shift + p
  - 输入 toggle sidebar position

- open enditors (打开的编辑器)
  - 其实我们可以通过 cmd + p 快速搜索文件，所以这部分如果想关掉，可以 Settings(Cmd+,) => 搜索 Explorer › Open Editors: Visible
    “打开编辑器”窗格中显示的编辑器的数量。将其设置为 0 将隐藏“打开编辑器”窗格 => 还有别的设置，可以更细粒度的控制这部分

#### 设置部分改成默认打开为 json

- cmd + , 搜索 Workbench › Settings: Editor 配置默认使用的设置编辑器 => 改为 json
- 如果想保留 UI 的快捷打开，可以在键盘快捷方式里面，open settings (ui)，可以自己设置一个，我设置成了（cmd + alt + ,）

#### peacock

- cmd + shift + P => peacock:enter a color
- settings 增加这两行，这样看起来颜色没那么鲜艳:
  "peacock.affectActivityBar": false
  "peacock.affectStatusBar": false

### 生产力提高技巧

#### 基本导航快捷键

- cmd + 0 焦点到 sidebar
- cmd + 1 焦点到编辑器
  下面几个都是英文首字母：
- cmd + shift + e 资源管理器 explorer
- cmd + shift + d 运行和调试 debug
- ctrl + shift + g 源代码管理器 git
- cmd + shift + x 扩展 extensions
- cursor 位置移动 —— On Mac: Ctrl + - ... navigate back / Ctrl + Shift + - ... navigate forward
- cmd + shift + o 如果是 markdown 文件，可以快速选择定位到哪个标题

#### Emmet

- 输入! （记住是英文输入法）然后 Tab 键
- 这个时候按 Tab 键，可以在标题和属性设置间切换，按序修改我们需要修改的地方
- (Cmd/Ctrl + Shift + P) and select "Emmet: Balance Outward" 可以一层层的选择标签
- (Cmd/Ctrl + Shift + P) and select "Emmet: Wrap with abbreviation" 可以可以快速在外层包标签(.test)
- (Cmd/Ctrl + Shift + P) and select "Format Document" 可以快速格式化文件,输入 format on save，可以选择是否要在保存时候格式化文档，推荐不要选，因为文件有差异，还是走具体项目的格式化
- emmet 样式上面，也可以用缩写，还是很好用的，省时间

#### auto close tag Extensions

可以安装这个插件，修改 tag 名的时候，闭合标签会跟着改动(根据说明配置 settings)
emmet 也可以达到这个=> cmd + shift + P ，输入 update tag

#### 移动，复制和删除

- 复制一行 opt/alt + shift + down/up arrow
- 移动一行 opt/alt + down/up arrow
- 删除一行 cmd + shift + k

vscode 里面，光标在哪一行，直接 cmd + c/x/v ,就可以复制/剪切了

#### folding sections

- html/code 光标放在需要折叠的区域 cmd + shift + P => fold
- fold region ，可以添加 a comment with //#region at the start of the block and //#endregion at the end.
  创建折叠区域
- cmd + k + 0，0 是代码折叠级别,全部折叠，同理可以换用 1，2，3
- cmd + k + j 展开所有代码块

#### 快速注释

- cmd + / 注释行

## Words

https://burkeholland.gitbook.io/vs-code-can-do-that/

- That denotes that these are separate workspaces, not folders. Other icon themes will not make this distinction as you can see below in Chalice Icons.
  这表示这些是独立的工作空间，而不是文件夹。其他图标主题不会做出这种区分，你可以在下面的 Chalice Icons 中看到。

- prerequisite | BrE priːˈrɛkwɪzɪt, AmE priˈrɛkwəzət |
  A. noun
  先决条件
  ▸ to be a prerequisite for sth;
  是某事的前提

- You can make some tweaks to the visual components of the editor to increase the available space and improve legibility.你可以对编辑器的视觉组件进行一些调整，增加可用空间，提高可读性。

- Here are a few more keyboard shortcuts to add to your repertoire( a list or supply of dramas, operas, pieces, or parts that a company or person is prepared to perform).

## ts

### ts 支持，但是目前首行报错
vetur.experimental.templateInterpolationService

### <script setup>
如果使用了<script setup>
用 Volar
禁掉 Vetur