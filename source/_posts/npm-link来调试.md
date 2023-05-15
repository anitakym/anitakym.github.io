---
title: npm-link来调试
date: 2020-08-05 16:59:13
tags: 
    - npm 系列
---
> 主体项目拆分出了UI库和核心逻辑js库，在UI库里面调试阶段，除了example，可能还得连具体代码，所以利用npm link进行调试

在被引用的包项目里面运行，执行之后，被引用的包会被链接到全局，路径是 {prefix}/lib/node_modules/<package>
```
npm link
```
在用包的项目里面运行,这样被引用的包会被链接到用包项目的node_modules下面
```
npm link seal_topic_ui
```

之后，只要在被引用包里面有修改，修改会直接生效


#### tips:查看prefix
```
npm config get prefix
```

#### 最佳实践
`npm link` 是一个非常有用的命令，它可以帮助开发者在本地开发和测试 Node.js 的模块或者 CLI 工具。`npm link` 可以在全局和本地项目之间创建一个符号链接，这使得开发者可以在不发布和安装 npm 包的情况下进行开发和测试。下面是一些使用 `npm link` 的最佳实践。

1. 在开发模块时使用`npm link`：

   首先，导航到要链接的项目目录：

   ```
   cd /path/to/your/module
   ```

   然后，在项目根目录下运行命令：

   ```
   npm link
   ```

   这将在全局 node_modules 目录下创建一个符号链接。（你可以通过运行 `npm root -g` 查找全局 node_modules 目录。）

   接下来，在你的依赖模块项目中使用 `npm link your-module` 来创建一个指向刚刚链接的模块的符号链接。将 `your-module` 替换为模块的名称。

   ```
   cd /path/to/your/dependent/project
   npm link your-module
   ```

   现在，在依赖项项目中，更改模块的代码和功能都会实时反映出来。

2. 在开发 CLI 工具时使用`npm link`：

   如果你正在开发一个 CLI 工具，则可以将其链接到全局路径，使其能够在本地生效。

   ```
   cd /path/to/your/cli/tool
   npm link
   ```

   这时，你就可以在终端中使用这个命令（CLI 工具）了，任何对工具的更改都会即时更新。

3. 从全局环境中取消链接：

   如果你想从全局环境中删除链接，可以在 `npm link` 的反向操作中使用 `npm unlink` 命令：

   ```
   cd /path/to/your/module
   npm unlink
   ```

   然后，在依赖目录中取消链接：

   ```
   cd /path/to/your/dependent/project
   npm unlink your-module
   ```

4. 使用 .npmrc 配置文件：

使用 `.npmrc` 配置文件可以轻松地将有关链接的配置应用于所需项目。例如，在全局 node_modules 目录中指定一个特定的位置。

在以上示例中，在全局 npm 配置文件（你可以用 `npm config ls` 或者 `npm config edit` 找到它）的路径下添加以下行：

```
prefix = /path/to/your/custom
     
```

5. `npm link` 时请注意版本冲突。因为 `npm link` 是在全局环境中创建了链接，确保在多个项目之间共享同一份代码时，不会引入不同版本的包。

6. 为了避免安全问题，请不要在生产环境下使用 `npm link`。当你在生产环境部署代码时，请始终使用 `npm install`。`npm link` 的主要目的是为了在开发过程中提高效率和便利性。

遵循这些最佳实践，你可以更高效地使用 `npm link` 进行 Node.js 项目的开发和测试。