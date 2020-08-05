---
title: git总结
date: 2020-05-18 18:04:56
tags: 
    - 工作经验总结系列
    - git系列
---

> 每天和git打交到的时间算是前几位了，总结一些问题，不断更新。。。

- 技术层面 git help XXX 能解决几乎所有疑惑，经验方面，遇到和解决的问题越多，思考也就越多；团队管理和规范推行方面，充分尊重工程师的感受，考虑团队的情况
#### 看过很多项目，或者解决定位线上问题 —— 快速清理无用的调试工作区
```
git clean
git checkout --
```


#### gitlab项目管理
分支保护（代码提交合并权限问题）

settings => repositoryprotected branches => expand

https://mirrors.edge.kernel.org/pub/software/scm/git/docs/git.html


gitlab continuous integration
http://gitlab.staff.xdf.cn/seal/js/seal_basics_ui/settings/integrations

#### 分支名称自动补全
指路：https://ohmyz.sh/（oh my zsh）


#### git 清除本地无远端的分支（清除本地所有分支）



#### 迁了一次仓库，团队人员变迁，所以目前一些项目的文档和说明及package.json不是很准确
git remote show origin


#### rebase/merge
推rebase的经验，可以写一篇小论文了。。。
rebase伴侣 => --force-with-lease