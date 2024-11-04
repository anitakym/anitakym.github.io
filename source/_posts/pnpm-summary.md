---
title: pnpm-summary
date: 2024-07-26 16:41:16
tags:
---
如果一个项目：
	"packageManager": "pnpm@8.10.2",
指定了pnpm版本
需要先npm切换到对应的npm版本，然后npm i -g pnpm

再执行pnpm install

``` .npmrc
这两个设置是与 JavaScript 包管理工具 pnpm 相关的配置选项。它们分别用于处理包提升和对等依赖的行为。

shamefully-hoist=true
作用: 这个选项会将所有的依赖提升到项目的根目录下，以便它们像 node_modules 里那样被直接访问。
背景: pnpm 默认使用一种“扁平化”依赖树的安装方法，各个包之间不会过于依赖于彼此的结构，从而减少重复安装和磁盘空间占用。但这种方法有时会导致某些模块无法找到其所需的依赖。
用途: 开启 shamefully-hoist=true 后，会调整依赖结构，使得与 npm 传统的 node_modules 树更相似，从而解决某些因包依赖树过于严格而引发的兼容性问题。
strict-peer-dependencies=false
作用: 这一选项决定对等（peer）依赖的安装策略。当设置为 false 时，pnpm 不会在对等依赖关系未满足的情况下报错。
背景: 对等依赖（peer dependencies）是指某些包在工作时需要与特定版本的另一个包一同使用。pnpm 默认情况下会严格检查这些关系，如果未找到相应的对等依赖则会报错。
用途: 设置 strict-peer-dependencies=false 后，即使对等依赖不能满足，安装过程仍然可以继续。这在某些情况下可以避免阻止安装的麻烦，确保开发的顺畅。如果项目仍可正常运行，此选项可以提供较大的灵活性。
如何配置这些选项
你可以通过创建或编辑项目根目录中的 .npmrc 文件来配置这些选项。以下是在 .npmrc 中添加这两个配置项的示例：

plaintext
# .npmrc 文件
shamefully-hoist=true
strict-peer-dependencies=false
示例与解释
假设你有一个 JavaScript 项目，其中有一些依赖在某些环节上存在兼容性问题：

plaintext
my-app/
├── node_modules/
├── .npmrc
├── package.json
└── src/
    └── index.js
通过 .npmrc 文件添加以上配置项，pnpm 将会调整包依赖安装的行为，以确保项目按需运行。

实际应用场景
1. shamefully-hoist=true
项目A依赖于某个老版本的库，并且一些模块是硬编码地依赖于全局的node_modules 结构。

示例：

项目依赖（package.json）：
json
{
  "dependencies": {
    "legacy-package": "^1.0.0",
    "modern-package": "^2.0.0"
  }
}
legacy-package 可能假定其某些依赖要在全局可用，正常情况下现代包管理工具（如pnpm）会将它们放到更加扁平化的结构里。

当你设置 shamefully-hoist=true 时，pnpm 将会提升这些依赖，使其兼容于老的 node_modules 查找方式。

2. strict-peer-dependencies=false
对等依赖的版本要求可能不十分严格，但如果每次安装都因这个原因失败，会浪费大量的时间和精力。

示例：

项目依赖（package.json）：
json
{
  "dependencies": {
    "package-a": "^1.0.0",
    "package-b": "^2.0.0"
  },
  "peerDependencies": {
    "react": "^17.0.0"
  }
}
某些包可能指定了对等依赖 react 的具体版本。如果项目使用的 package-b 偶尔与该版本不完全匹配，在引入 strict-peer-dependencies=false 后，安装不会因不完全匹配而立即失败，这样你可以继续进行后续的开发或者手动调整依赖关系。

总结
配置项 shamefully-hoist=true 和 strict-peer-dependencies=false 提供了对 pnpm 包依赖管理的更大灵活性，可以帮助你解决某些复杂或不兼容性的依赖问题。利用这些选项，可以确保项目按预期安装和运行，增强开发者在复杂依赖环境中的控制力。