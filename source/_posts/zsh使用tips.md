---
title: zsh使用tips
date: 2020-08-06 15:41:21
tags:
    - 工具篇
---
> 从 macOS Catalina 版开始，zsh (Z shell) 是所有新建用户帐户的默认 Shell。
bash 是 macOS Mojave 及更低版本中的默认 Shell。(https://support.apple.com/zh-cn/HT208050)

> 终端中输`man zsh` 即可了解更多，这篇主要聊聊 `oh my zsh` (指路官网: https://ohmyz.sh/)

#### 安装
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

tips:如果遇到了网络问题，可以配置下映射
```
199.232.68.133 raw.githubusercontent.com
```

> 即装即用，git马上就能自动补全分支名称了（为什么呢？）我们看下官方模块中的插件部分
<pre>
git-auto-fetch
git-escape-magic
git-extras
git-flow-avh
git-flow
git-hubflow
git-prompt
git
gitfast
github
gitignore
</pre>
再查看下.zshrc文件
```
➜  ~ cat .zshrc | grep git
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
# Example format: plugins=(rails git textmate ruby lighthouse)
plugins=(git)
```
想要配置更多功能，把插件名字加到zshrc文件里面即可,空格隔开
```
plugins=(git gitignore)
```