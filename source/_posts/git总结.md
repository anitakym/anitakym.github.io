---
title: git总结
date: 2020-05-18 18:04:56
tags:
  - 工作经验总结系列
  - git系列
---

> 每天和 git 打交到的时间算是前几位了，总结一些问题，不断更新。。。

- 技术层面 git help XXX 能解决几乎所有疑惑，经验方面，遇到和解决的问题越多，思考也就越多；团队管理和规范推行方面，充分尊重工程师的感受，考虑团队的情况

#### 看过很多项目，或者解决定位线上问题 —— 快速清理无用的调试工作区

```
git clean
git checkout --
```

#### gitlab 项目管理

分支保护（代码提交合并权限问题）

settings => repositoryprotected branches => expand

https://mirrors.edge.kernel.org/pub/software/scm/git/docs/git.html

gitlab continuous integration
/settings/integrations

#### 分支名称自动补全

指路：https://ohmyz.sh/（oh my zsh）

#### git 清除本地无远端的分支（清除本地所有分支）

- 强制删除所有分支
  `git branch |xargs git branch -D`

- 本地修改过未提交的不会删除
  `git branch |xargs git branch -d`

#### 迁了一次仓库，团队人员变迁，所以目前一些项目的文档和说明及 package.json 不是很准确

git remote show origin

#### rebase/merge

推 rebase 的经验，可以写一篇小论文了。。。
rebase 伴侣 => --force-with-lease

文档指南：
重写历史的时候可以使用的命令及需要注意什么
https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History

#### git 报错分析

```
error: src refspec master does not match any.
error: failed to push some refs to 'https://github.com/anitakym/blog.git'
```

没有提交内容，要 add 和 commit （引起该错误的原因是，目录中没有文件，空目录是不能提交上去的）

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

### 查看 working tree 的状态

git-status - Show the working tree status
切换分支的时候，注意查看

### gitk(the git repository browser)

https://git-scm.com/docs/gitk/

### .gitignore 规则生效

如果一旦纳入版本管理，可以先删除本地缓存，然后提交

```
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```

.gitignore 参考
https://docs.github.com/en/github/getting-started-with-github/getting-started-with-git/ignoring-files

### 导出某个项目的作者

```
"authors": "git log --format='%aN <%aE>' | sort -u > AUTHORS"
```

### 新建项目

rm -rf .git

### 项目过大问题，或者误提交大文件

```
# 找出大文件
git verify-pack -v .git/objects/pack/pack-*.idx | sort -k 3 -g | tail -5
# 找出对应文件位置名称，XXX为第一步查出来的第一列的hash
git rev-list --objects --all | grep XXXXXXXXXXXX
# 用filter-branch 清理文件
git filter-branch --index-filter 'git rm --cached --ignore-unmatch <your-file-name>'
# 系列操作
rm -rf .git/refs/original/
git reflog expire --expire=now --all
git fsck --full --unreachable
git repack -A -d
git gc --aggressive --prune=now
git push --force [remote] master
```

### 跨项目关联推送分支

A 是模版项目
B 是用了模版项目的业务项目

- 模版项目 A 更新了基础配置，可以切一个分支，feature/update-basic
- 在 B 中也新建一个分支 feature/update-basic
- 将 A 的远端源切换成 B
- 推送本地 feature/update-basic 分支到远端即可

### 修改提交 message

切记，如果推送到了远端，保证一定不是协作分支，不然最好确保都是本地操作

```
# 显示倒数n次的commit msg
git rebase -i HEAD~n
# 要修改哪个，就把pick改成edit
git commit --amend
# 改完之后保存并退出
git rebase --continue
```

### 关联远端仓库
```
# 先查看下
git remote -v
# 再设置
git remote remove origin
git remote add origin xxx
# 都可
git remote set-url origin xxx
```

### tag
文档指路：https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%89%93%E6%A0%87%E7%AD%BE、
```
# 引自文档
Git 支持两种标签：轻量标签（lightweight）与附注标签（annotated）。

轻量标签很像一个不会改变的分支——它只是某个特定提交的引用。

而附注标签是存储在 Git 数据库中的一个完整对象， 它们是可以被校验的，其中包含打标签者的名字、电子邮件地址、日期时间， 此外还有一个标签信息，并且可以使用 GNU Privacy Guard （GPG）签名并验证。 通常会建议创建附注标签，这样你可以拥有以上所有信息。但是如果你只是想用一个临时的标签， 或者因为某些原因不想要保存这些信息，那么也可以用轻量标签。
```
```
# annotated
git tag -a v1.0.1 -m "for sth, update sth"
git show v1.0.1
# lightweight
git tag v1.0.2
git tag
# 对某个提交打标签
git tag -a v1.0.3 xxxxx-commit-hash
# 推送
git push origin --tags
# 删除
git tag -d v1.0.1
git push origin --tags
# 删除
git push origin --delete v1.0.1

```