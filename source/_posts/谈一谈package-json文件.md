---
title: 谈一谈package-json文件
date: 2020-10-22 11:06:19
tags:

---

> 官方文档指南：https://docs.npmjs.com/files/package.json

### version 
- semver - 见```软件版本```博文
### main 属性
- 项目入口 （被import｜require，默认入口main指定）
- 如果不填的话，默认是找文件夹根目录下的index
<pre>
The main field is a module ID that is the primary entry point to your program. That is, if your package is named foo, and a user installs it, and then does require("foo"), then your main module’s exports object will be returned.

This should be a module ID relative to the root of your package folder.

For most modules, it makes the most sense to have a main script and often not much else.
</pre>
- 一般用于对外提供调用功能的API入口

### scripts
- 带有命令行的node模块，不需要全局安装，scripts中定义的脚本根据node_modules找到对应模块并启动脚本指令

### keywords | author | license
### TIPS
#### 中文字符
- Package.json 里面不要出现中文，不然会出现解析错误
-项目标题不要大写字母，要全小写


### json
- https://www.json.org/json-zh.html
```
A value can be a string in double quotes, or a number, or true or false or null, or an object or an array. These structures can be nested.
```
- 注意double quotes,双引号

### -lock文件
如果没有强制配 --registry，registry会走lock文件里面的，即使强制配置了--registry还是会走lock
我这边会ignore -lock文件
```
npm WARN old lockfile 
npm WARN old lockfile The package-lock.json file was created with an old version of npm,
npm WARN old lockfile so supplemental metadata must be fetched from the registry.
npm WARN old lockfile 
npm WARN old lockfile This is a one-time fix-up, please be patient...
npm WARN old lockfile 
```
切换了node版本后，lockfile也会被重写

```
npm ERR! code ERESOLVE
npm ERR! ERESOLVE unable to resolve dependency tree
npm ERR! 
npm ERR! While resolving: xxx
npm ERR! Found: react@17.0.2
npm ERR! node_modules/react
npm ERR!   react@"^17.0.1" from the root project
npm ERR! 
npm ERR! Could not resolve dependency:
npm ERR! peer react@"^0.14.0 || ^15.0.0 || ^16.0.0-0" from react-html-parser@2.0.2
npm ERR! node_modules/react-html-parser
npm ERR!   react-html-parser@"^2.0.2" from the root project
npm ERR! 
npm ERR! Fix the upstream dependency conflict, or retry
npm ERR! this command with --force, or --legacy-peer-deps
npm ERR! to accept an incorrect (and potentially broken) dependency resolution.
```
这个是因为node版本切换高了
```
> ttf2woff2@3.0.0 install /home/xxx/Documents/xxx/current/seal_pdf_server/node_modules/ttf2woff2
> ((node-gyp configure && node-gyp build) > builderror.log) || (exit 0)

make: g++: No such file or directory
make: *** [addon.target.mk:137: Release/obj.target/addon/csrc/addon.o] Error 127
gyp ERR! build error 
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/home/xxx/.nvm/versions/node/v14.20.0/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:194:23)
gyp ERR! stack     at ChildProcess.emit (events.js:400:28)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (internal/child_process.js:285:12)
gyp ERR! System Linux 5.18.11-200.fc36.x86_64
gyp ERR! command "/home/xxx/.nvm/versions/node/v14.20.0/bin/node" "/home/xxx/.nvm/versions/node/v14.20.0/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "build"
gyp ERR! cwd /home/xxx/Documents/xxx/current/seal_pdf_server/node_modules/ttf2woff2
gyp ERR! node -v v14.20.0
gyp ERR! node-gyp -v v5.1.0
gyp ERR! not ok
```
用的之前的lockfile,报了这个错误；删除之前lockfile之后依然还是有这个错误
- This is a NodeJS wrapper for the Google WOFF2 project. If the C++ wrapper compilation fail, it fallbacks to an Emscripten build.
- https://insertafter.com/en/blog/native-node-module.html
```
Gracefully fail compilation
So, now we have our Emscripten build, let's fallback to him when the native NodeJS add-on compilation goes wrong. First, we must ensure that any failure won't impeach the module to install. We're basically doing this by overriding the default installation script to exit with a 0 code whatever result the compiler gives.

Then, as a main JavaScript file we will ensure failing to bind to the native add-on will result in requiring the Emscripten fallback. It is simply done by catching exceptions when requiring the bindings.
```
- 这样就确保任何失败都不会影响模块的安装 - 通过覆盖默认的安装脚本来做到这一点，无论编译器给出什么结果，都以0代码退出
- 然后，绑定时通过捕捉异常回退到Emscripten


### files
- 如果不写的话，所有文件都会被打包进去
- 写的话，就是当我们的包作为依赖包被安装时候，被包括的条目


### lock
`package-lock.json` 文件是在 Node.js 项目中使用 npm 包管理器时自动生成的。 它记录了关于项目依赖项（如名称、版本、来源等信息）的确切版本。`lockfileVersion` 是表示锁定文件版本的属性。

每个 `lockfileVersion` 版本都对应一个 npm 版本。 在 `lockfileVersion` 不同之间，主要区别在于文件和解析方式的细微差别

1. `lockfileVersion: 1`
   - 对应于 npm v5 和 v6。
   - 此版本的主要目标是确保具有兼容性，使那些正在使用较旧版本的用户不受升级项目依赖版本和生成新锁定文件影响。
   - 使用此版本时，项目依赖性树在 `package-lock.json` 中以层次结构表示。

2. `lockfileVersion: 2`
   - 对应于 npm v7 之后的版本。
   - 包含新的项目依赖关系解析算法。
   - 包含对 `workspaces` 的支持。
   - 使用此版本时，项目依赖性树使用扁平列表表示，而不是层次结构。 这使得锁定文件更紧凑，并有助于减小文件大小。

除了 `lockfileVersion`，`package-lock.json` 中还包括以下属性：

- `name` 和 `version`：补充 `package.json` 中项目名称和版本的信息。
- `requires`：到处都是，作为所有依赖。 这些依赖在 `dependencies` 下的该依赖对象中。
- `dependencies`：项目的所有第三方依赖，包括直接和间接依赖。 每个依赖包含名称、版本、来源等信息。 还可以包括指向子依赖项的 `requires` 和 `dependencies`。

维护 `package-lock.json` 文件的最佳实践是将它包含在您的版本控制系统中。 这样可以确保所有团队成员和不同环境之间使用相同的依赖项版本。

### peer dep
在 npm 中，`npm i`（或 `npm install`）命令用于安装项目的依赖项。`--legacy-peer-deps` 是一个命令行选项，用于在安装依赖项时使用旧版的 peer 依赖处理逻辑。

当您使用 npm v7 及更高版本时，默认情况下，peer 依赖项将自动安装，并在遇到冲突时中止安装并报错。这是为了确保所有依赖项与其 peer 依赖项完全兼容，避免后续的问题。

然而，某些情况下，自动安装并检查 peer 依赖()可能会导致错误，或者与现有项目的配置不兼容。在这种情况下，使用 `--legacy-peer-deps` 选项可以按照旧版 npm（v6 及以下版本）的逻辑处理 peer 依赖。也就是说，npm 将不会自动安装 peer 依赖项，也不会因 peer 依赖项冲突而中止安装过程。

一个使用 `--legacy-peer-deps` 的例子：

```
npm i --legacy-peer-deps
```

该命令将使用旧版 npm 的逻辑来处理和安装项目的依赖项及其 peer 依赖。当您在更新一个较旧的项目时，或者遇到 peer 依赖冲突导致无法安装新依赖时，这个选项可能会有所帮助。