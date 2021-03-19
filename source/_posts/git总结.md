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
* 强制删除所有分支
`git branch |xargs git branch -D`

* 本地修改过未提交的不会删除
`git branch |xargs git branch -d`


#### 迁了一次仓库，团队人员变迁，所以目前一些项目的文档和说明及package.json不是很准确
git remote show origin


#### rebase/merge
推rebase的经验，可以写一篇小论文了。。。
rebase伴侣 => --force-with-lease


#### git报错分析
```
error: src refspec master does not match any.
error: failed to push some refs to 'https://github.com/anitakym/blog.git'
```
没有提交内容，要add和commit （引起该错误的原因是，目录中没有文件，空目录是不能提交上去的）

### 重写历史需注意
https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%87%8D%E5%86%99%E5%8E%86%E5%8F%B2


### github/gitlab
```
curl -s <github_url> | vim -
```
通过管道把 curl 命令的输出传给 VIM，以方便在 VIM 中查看较长的输出。


### 好用的命令行工具
tig(https://jonas.github.io/tig/)
```
brew install tig
```