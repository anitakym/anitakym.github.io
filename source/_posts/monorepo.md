<!--
 * @Author: yimin kuang
 * @Date: 2024-04-15 10:04:03
 * @LastEditors: yimin kuang
 * @LastEditTime: 2024-06-18 18:13:39
 * @Description: 描述信息
-->
---
title: monorepo
date: 2022-03-18 17:46:25
tags:
---

> https://static.frontendmasters.com/resources/2020-10-15-js-typescript-monorepos/js-ts-monorepos.pdf
> https://github.com/mike-north/js-ts-monorepos/
- monorepo 在一个 git 仓库里管理多个项目
## v3
```
## Project Structure

This repository employs a [monorepo](https://en.wikipedia.org/wiki/Monorepo) setup which hosts a number of associated packages under the `packages` directory:

## Development Setup

You will need [Node.js](https://nodejs.org) **version 10+**, and [PNPM](https://pnpm.io).

We also recommend installing [ni](https://github.com/antfu/ni) to help switching between repos using different package managers. `ni` also provides the handy `nr` command which running npm scripts easier.

```

## element-plus

## typescript-eslint
- monorepo


## spectrum
- Install yarn: We use yarn to handle our JavaScript dependencies. (plain npm doesn't work due to our monorepo setup) See the yarn documentation for instructions on installing it.


## xstate
- https://github.com/statelyai/xstate


## notesnook 开源的笔记软件 - 对标evernote
- https://github.com/streetwriters/notesnook


### lerna
- Lerna是一个快速、现代的构建系统，用于管理和发布来自同一资源库的多个JavaScript/TypeScript包。

### pnpm
- workspace
- pnpm install --recursive

### yarn workspace
- 主流方案是lerna + yarn worksapce，lerna负责发布和版本升级，yarn workspace负责依赖管理

### npm
- 是的，npm 也支持 monorepo。随着 npm 7 发布，在 npm 自带的工具集中新增了名为 workspaces 的功能，它能够帮助用户更好地管理 monorepo。

要在 npm 中设置 monorepo，您需要在项目的顶层创建一个包含 workspaces 属性的`package.json`文件。此属性应包含一个数组，指明所有工作空间的相对路径。例如：

```json
{
  "name": "my-monorepo",
  "private": true,
  "workspaces": ["packages/*"]
}
```

在这个例子中，项目的所有子包都存放在`packages/`目录下。

为了更好地管理 monorepo，您可以选择使用像 Lerna 这样的第三方工具。Lerna 和 npm workspaces 结合使用，能够让用户在 monorepo 中更方便地管理依赖和发布包。如果您决定使用 Lerna，请确保将`lerna.json`文件放在项目的根目录下。在 Lerna 中，你还可以根据需要为 monorepo 中的每个模块建立符号链接，从而让这些模块可以直接引用其他模块的源代码，而不是已发布的 npm 包版本。

### monorepo - nest
微服务项目

### nx


### rushstack

### 
Setup
This repo uses pnpm, but should work fine with any of the following:

yarn workspaces
npm 7 workspaces
npm < 7 and lerna bootstrap
I strongly recommend pnpm over the other solutions, not only because it's usually faster, but because it avoids dependency problems caused by hoisting (see https://github.com/NiGhTTraX/ts-monorepo/commit/d93139166b25fab15e9538df58a7d06270b846c9 as an example).

# Install pnpm with your preferred method: https://pnpm.io/installation.
npm i -g pnpm

# Install all dependencies.
pnpm i

https://github.com/NiGhTTraX/ts-monorepo/commit/d93139166b25fab15e9538df58a7d06270b846c9

 nvm use v18.20.2 
Now using node v18.20.2 (npm v10.5.0)
➜  seal_backend_increase git:(feature/productManage) pnpm -v
9.1.4
➜  seal_backend_increase git:(feature/productManage) nvm use v16.19.1 

Now using node v16.19.1 (npm v8.19.3)
➜  seal_backend_increase git:(feature/productManage) 
➜  seal_backend_increase git:(feature/productManage) pnpm -v         
Type Error: URL.canParse is not a function
    at isSupportedPackageManagerDescriptor (/Users/.nvm/versions/node/v21.7.3/lib/node_modules/corepack/dist/lib/corepack.cjs:23037:15)
    at Engine.resolveDescriptor (/Users/.nvm/versions/node/v21.7.3/lib/node_modules/corepack/dist/lib/corepack.cjs:23393:10)
    at executePackageManagerRequest (/Users/.nvm/versions/node/v21.7.3/lib/node_modules/corepack/dist/lib/corepack.cjs:24233:41)
    at async BinaryCommand.validateAndExecute (/Users/.nvm/versions/node/v21.7.3/lib/node_modules/corepack/dist/lib/corepack.cjs:21173:22)
    at async _Cli.run (/Users/.nvm/versions/node/v21.7.3/lib/node_modules/corepack/dist/lib/corepack.cjs:22148:18)
    at async Object.runMain (/Users/.nvm/versions/node/v21.7.3/lib/node_modules/corepack/dist/lib/corepack.cjs:24279:12)
➜  seal_backend_increase git:(feature/productManage) 