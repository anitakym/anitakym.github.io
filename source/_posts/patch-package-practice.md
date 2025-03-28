---
title: patch-package-practice
date: 2023-11-07 13:37:20
tags:
---
## 处理问题
https://github.com/ds300/patch-package

- 依赖的第三方包代码有问题，需要更新，最便捷的的方式

`patch-package` 是在依赖包中进行小规模更改后，可以用来记录并复制这些更改的工具。以下是使用`patch-package`的最佳实践：

1. 安装patch-package: 可以使用npm或yarn进行安装。
   
   使用npm: `npm i patch-package postinstall-postinstall`
   
   使用yarn: `yarn add patch-package postinstall-postinstall`

2. 创建补丁: 先进行对依赖包的修改，然后运行`npx patch-package package-name`。

3. 尽可能小的改动: 不要尝试使用patch-package进行大规模的更改。这可能导致版本升级时patch失败，甚至可能违反包的许可证。

4. 使用git版本控制: 在使用patch-package之前，最好首先进行一次git commit，以便在产生一个补丁文件后，可以清楚地看到新增的更改。

5. 在`postinstall`脚本中运行`patch-package`: 在`package.json`的`scripts`属性中添加一项 `"postinstall": "patch-package"`。这样做可以确保每次安装或更新依赖后都会自动应用补丁。

6. 应用`yarn.lock` 或 `package-lock.json`: 这样做以确保将来的构建将使用相同的依赖项版本，并且补丁将应用。

7. 切勿修改`node_modules`中包的源代码: 使用`patch-package`之前，一定要先在源代码中进行修改，然后再创建补丁文件。

8. 提交patch文件到版本控制系统: 这样做以便其他开发者在`npm install`后能够应用同样的补丁。

9. 在升级依赖项时小心: 当你升级一个已经打过补丁的包时，确保测试，因为补丁可能不再适用于新版本。

记住，在修改一个包时，最好的选择通常是先提交一个pull请求到上游项目。然而，如果你需要快速修复问题，或者你的更改不太可能被上游项目接受，那么`patch-package`是一个非常有用的工具。

```
用户遇到了通常有两种解法
1）patch-package 临时改
2）等官方（框架层或 click-to-react-compnent）发版修复

框架层也有几个解法
1）给 cnpm 提 bug version
2）Umi 锁版本修复

把 require.resolve('click-to-react-component') 写到了 Umi 插件 Hook 的外面，导致注册时即执行。于是又提了个 PR 修复这个问题，让这个插件的任何功能都不影响生产构建。
```