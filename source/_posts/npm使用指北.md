---
title: npm使用指北
date: 2021-03-17 14:48:34
tags:
---

查看全局安装的包的版本
```
npm list -g --depth 0 | grep @vue/cli
```

### 问题处理
(node:50731) ExperimentalWarning: Package name self resolution is an experimental feature. This feature could change at any time
94% after seal[hardsource:a9cf9509] Could not freeze ./src/router/index.js: Cannot read property 'hash' of undefined
98% after emitting

### error
```
UNMET PEER DEPENDENCY webpack@4.x.x || 5.x.x

npm ERR! peer dep missing: webpack@4.x.x || 5.x.x, required by webpack-cli@4.9.2
npm ERR! peer dep missing: webpack@4.x.x || 5.x.x, required by @webpack-cli/configtest@1.1.1
npm ERR! extraneous: which@2.0.2 /Users/xxxxx/node_modules/cross-spawn/node_modules/which
```
#### peer dep
- https://blog.domenic.me/peer-dependencies/

### n
n升级到lts的时候出了问题

node -v
dyld: initializer function 0x0 not in mapped image for /usr/local/bin/node

brew uninstall --force node
brew uninstall icu4c && brew install icu4c
brew unlink icu4c && brew link icu4c --force
brew install node

I recently encountered a similar issue (after doing brew switch node 9.8.0 to downgrade to a previous version of node)

dyld: Library not loaded: 
/usr/local/opt/icu4c/lib/libicui18n.60.dylib
  Referenced from: /usr/local/bin/node
  Reason: image not found
Abort trap: 6
The issue is that node is picky about which version of icu4c it's looking for, and the version I had installed (62) was higher than node was expecting.

To fix, I made sure I had version 60 of icu4c selected.

First I found which versions I had with brew info icu4c, then did brew switch icu4c 60.2 to select the one node was expecting.

重新官网下载了node,解决的
https://nodejs.org/en/

### npx
可以通过npx,去执行cli命令，不需要额外的安装
比如：
```
npx create-next-app test-demo
npx create-react-app test-app
(If you've previously installed create-react-app globally via npm install -g create-react-app, we recommend you uninstall the package using npm uninstall -g create-react-app or yarn global remove create-react-app to ensure that npx always uses the latest version.)
```
npx主要用于命令行寻址等辅助功能上

- 可以和degit(https://www.npmjs.com/package/degit)配合着使用，比如：https://github.com/antfu/vitesse/blob/main/README.zh-CN.md
```
npx degit antfu/vitesse my-vitesse-app
cd my-vitesse-app
pnpm i # 如果你没装过 pnpm, 可以先运行: npm install -g pnpm
```

### yarn
可以通过homebrew安装，也可以通过npm安装
https://yarnpkg.com/getting-started
yarn autoclean 功能可以试试

https://gist.github.com/jonlabelle/c082700c1c249d986faecbd5abf7d65b
https://shift.infinite.red/npm-vs-yarn-cheat-sheet-8755b092e5cc
这篇文章提供npm和yarn的对比：
官方也有简单的vs：
https://classic.yarnpkg.com/en/docs/migrating-from-npm
```
npm install === yarn
npm installl testpackage --save === yarn add testpackage
npm uninstall testpackage --save === yarn remove testpackage
npm install testpackage --save-dev === yarn add testpackage --dev
npm update --save === yarn upgrade
```
```
// 都一样的
init | link | outdated | publish | run | cache clean | login | test
```
```
// yarn 有npm没有的
yarn licenses list
yarn why lodash
```

### node_modules/.bin
```
通过npm启动的脚本，会默认把node_modules/.bin加到PATH环境变量中
https://docs.npmjs.com/cli/v7/commands/npm-run-script

当某个模块配置了 bin 定义时，就会被安装的时候，自动软链了过去
https://docs.npmjs.com/cli/v7/configuring-npm/package-json/#bin
```

### .npmrc
可以先看下```npm config ls -l```
https://docs.npmjs.com/cli/v7/configuring-npm/npmrc
<pre>
具体项目：
registry 可以在这个里面设置

可以设置
package-lock=false
koa就是这么设置的
// 说明:如果设置为false，那么在安装时将忽略package-lock.json文件
package-lock
Default: true
Type: Boolean
If set to false, then ignore package-lock.json files when installing. This will also prevent writing package-lock.json if save is true.

When package package-locks are disabled, automatic pruning of extraneous modules will also be disabled. To remove extraneous modules with package-locks disabled use npm prune.
</pre>

### pnpm
- https://pnpm.io/zh/motivation
- pnpm - 依赖项将存储在一个内容可寻址的仓库中
- npm - 依赖都会被提升到模块的根目录 - 扁平化结构
- pnpm - 使用软链的方式将项目的直接依赖添加进模块文件夹的根目录。 
```
树形的问题：
This approach had two serious issues:
- frequently packages were creating too deep dependency trees, which caused long directory paths issue on Windows
- packages were copy pasted several times when they were required in different dependencies
To solve these issues, npm rethought the node_modules structure and came up with flattening. 
```
- 推荐阅读：https://www.kochan.io/ 这个里面写了几篇文章
- vue-next用pnpm,还在preinstall里面加了验证
- vite - only allow pnpm
#### peerDependencies
- npm中 ： https://docs.npmjs.com/cli/v9/configuring-npm/package-json#peerdependencies
- pnpm: https://pnpm.io/zh/how-peers-are-resolved
### difference
- https://mp.weixin.qq.com/s?__biz=Mzg4MTYwMzY1Mw==&mid=2247496601&idx=1&sn=4c3bc00c37163e1dca152ebb8f723619&source=41#wechat_redirect

## 项目管理
### init
- ```npm init```

### package.json
见```谈一谈package-json文件```博文


### 技术选型
- https://npmtrends.com/
- 可以看trends参考


### npm-cache
- https://docs.npmjs.com/cli/v8/commands/npm-cache
- clean: Delete all data out of the cache folder. Note that this is typically unnecessary, as npm's cache is self-healing and resistant to data corruption issues.

### --verbose 
- 在较慢的网络上, 最好使用 --verbose 标志来显示下载进度: `npm install --verbose electron`
- 在运行 npm install electron 时，有些用户会偶尔遇到安装问题。在大多数情况下，这些错误都是由网络问题导致，而不是因为 electron npm 包的问题。 如 ELIFECYCLE、EAI_AGAIN、ECONNRESET 和 ETIMEDOUT 等错误都是此类网络问题的标志。 最佳的解决方法是尝试切换网络，或是稍后再尝试安装


### npm info

### npm 发布(普通模块｜二进制模块)
```
npm login
nrm use npm
npm publish
```
```
npm i -g np
np
```

### packages 
- kp is a tool for kill process by server port. it can be used on mac && linux && window
- mongo-here

### process.argv 解析
- clipanion
- commander.js
- yargs

### .npmignore
```
`.npmignore` 文件是在发布 npm 包时排除不必要文件的一种方法。排除这些文件有助于减小包的体积，从而提高安装速度并减少磁盘空间占用。以下是一些建议的最佳实践：

1. **基本规则**：通过将通配符（例如 `*`）或文件/文件夹名称添加到 `.npmignore`，您可以从发布的 npm 包中排除这些特定文件或文件夹。

2. **将测试文件排除在外**：通常，用户不需要您的测试文件。将测试文件夹添加到 `.npmignore` 中（如 `test/`, `__tests__/` 等）。

3. **排除配置文件和工具**：开发工具、构建工具和测试工具的配置文件不应包含在发布的 npm 包中。可能的文件包括：`.eslintrc`, `.prettierrc`, `.editorconfig`, `.gitignore` 等。

4. **排除文档和代码示例**：文档和示例代码可以用来进一步解释包的使用方法，但在发布时应排除。文件夹名称可能包括：`docs/`, `examples/`, `samples/` 等。

5. **排除源代码和构建产物**：如果您的项目使用了编译步骤（如使用 TypeScript、Babel 或构建工具），请排除源代码和生成的构建产物。可能的文件包括 `src/`, `dist/`, `build/`，但如果 `dist/` 或 `build/` 中的文件是最终用户需要的，则不要排除它们。

6. **优先使用 `.npmignore` 而非 `files` 属性**：虽然 `package.json` 中的 `files` 属性可以指定要发布的文件，但使用 `.npmignore` 更方便管理排除列表。对于大型项目，`.npmignore` 的管理成本较低。

7. **保留 LICENSE 和 README**：即使这些文件不是绝对必要的，我们还是建议您将许可证（LICENSE）和自述文件（README.md）包含在发布的 npm 包中，因为这些文件提供了关于您软件的许可、使用和贡献的重要信息。

8. **使用 `.gitignore` 作为备选方案**：如果您没有提供 `.npmignore` 文件，npm 会默认使用 `.gitignore` 来确定要排除哪些文件。这也是合理的选择，但最好明确提供 `.npmignore` 文件以避免潜在的配置混淆。

根据您的项目需求进行调整可能的文件/文件夹，确保发布的 npm 包尽可能小且只包含所需的内容。
```
### postinstall
Create React App：Facebook 出品的 React 脚手架工具， postinstall 用于提示用户将其加入到 PATH 环境变量中。

Gatsby：一个用于构建静态网站和应用程序的开源框架，它在 postinstall 中检查 Gatsby CLI 是否已经安装，若没有，则提示用户如何安装。

Angular CLI：Angular 官方推出的命令行工具，它使用 postinstall 创建提交时的拦截器，用于在提交代码时运行携带 --commit 模式。

sharp：一个高性能的 Node.js 图像处理库，在 postinstall 脚本中自动下载和安装预编译的二进制文件。

node-sass：Node.js 版本的 Sass 编译器，其 postinstall 用于处理跨平台安装，并在安装过程中下载对应平台所需的二进制文件。

`npm postinstall` 是一个 npm 生命周期钩子，它在安装包及其依赖项之后运行。这是一个强大的钩子，您可以利用它执行一些在安装后需要进行的操作。以下是在使用 `npm postinstall` 时要遵循的一些建议和最佳实践：

1. **避免过度使用**: 尽管 `postinstall` 具有很大的灵活性，但应避免将其用于不必要的操作。它最适合用于编译/构建代码、生成配置文件或执行其他需要在安装包之后执行的操作。

2. **将操作过程告知用户**: 在执行 `postinstall` 期间，如果有可能的话，请向用户显示操作进度、实时日志或相关提示。这有助于用户了解在安装过程中发生了什么，以及如何解决可能出现的问题。

3. **确保脚本可移植**: 在不同的操作系统和环境下，`postinstall` 脚本可能会表现不同。避免使用特定平台的命令或工具，以确保在各种环境中都能正常工作。

4. **优雅地处理错误**: 如果 `postinstall` 脚本无法执行某些操作，优雅地处理这些错误，并向用户提供有关发生问题的原因和可能的解决方案的信息。

5. **尽量提前中断**: 当检测到可能导致`postinstall`无法正常执行的问题时，尽量提前中断脚本。例如，通常应确保所有依赖项可用，然后再执行其他操作。

6. **考虑在安装某些可选依赖时使用 `postinstall`**: 如果某些依赖项是可选，可以利用 `postinstall`脚本来根据用户环境或需求进行下载。这将有助于减小初始安装文件的大小。

7. **避免进行不必要的网络活动**: 在`postinstall`过程中不建议下载或上传大量不必要的数据。仅在需要时才执行此类操作，以减少安装时间和带宽占用。

8. **确保兼容性**: 请确保您的 `postinstall` 脚本与不同版本的 Node.js 和 npm 兼容。如果必须要求特定版本，请在 `package.json` 中指定所需的 Node.js 和 npm 版本范围。

9. **不要破坏用户环境**: 不要在 `postinstall` 脚本中修改全局的 Node.js 安装和环境，并确保不要破坏用户设备上的其他软件和配置。

10. **在开发环境和生产环境之间做出区分**：根据需要，可以使用 `NODE_ENV` 环境变量来了解当前处于生产环境还是开发环境。在不同环境中选择相应的行为，如避免在生产环境中包含只在开发环境中才需要的文件。

遵循以上最佳实践，可以确保 `postinstall` 脚本在各种环境中正常工作，提供良好的用户体验，并避免对用户的环境产生不良影响。

### usr/local/bin/pnpm: line 8: 33087 Killed: 9
pnpm 进程在执行时被意外终止（Killed: 9）
1. 内存不足：系统可能由于资源限制（如内存不足）终止了进程。确保你的系统有足够的可用内存。
2. 权限问题：确保你有正确的权限运行 pnpm。根据你提供的路径（`/usr/local/bin/pnpm`），它应该是全局安装的。尝试以管理员身份（使用 sudo）运行 pnpm 命令，例如：
   ```
   sudo pnpm install
   ```
3. 确保正确安装了 Node.js 和 pnpm。运行以下命令以检查 Node.js 和 pnpm 的版本：
   ```
   node -v
   pnpm -v
   ```
   如果你看到这些命令中的任何一个调用失败或给出错误，请先解决这些错误。
4. 重新安装 pnpm，因为它可能已损坏或不完整。
   首先卸载 pnpm：
   ```
   npm uninstall -g pnpm
   ```
   然后重新全局安装 pnpm：
   ```
   npm install -g pnpm
   ```
用n装npm也是，也会给提示，也是权限问题；
