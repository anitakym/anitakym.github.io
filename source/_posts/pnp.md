---
title: pnp
date: 2024-10-22 17:11:18
tags:
---
Plug'n'Play (简称为 PnP) 是 Yarn 的一项功能，用于管理和加载 Node.js 的依赖关系。与传统的 node_modules 文件夹方法不同，PnP 通过直接引用依赖存储在的压缩文件 (zip) 来高效地管理依赖，从而提高性能和安全性。

PnP 的工作原理
在传统的 Node.js 项目中，Yarn 或 npm 会将所有的依赖下载并解压到 node_modules 文件夹中，这可能会导致：

文件夹嵌套过深。
存在大量重复的文件。
耗费大量磁盘空间和 I/O 操作时间。
PnP 通过以下方法简化了这一过程：

依赖关系的声明和解析:

所有依赖关系都不会被物理安装到 node_modules 文件夹中。
在项目的根目录会生成一个 .pnp.js 文件，该文件包含了所有依赖的元数据和解析逻辑。
载入依赖:

Node.js 会通过 .pnp.js 文件来解析模块路径，而不是查找实际的 node_modules 目录。
存储依赖:

依赖被存储在 .yarn/cache 文件夹中，通常存储为压缩文件 (zip)。
PnP 的优点
性能提升: 不用遍历 node_modules 目录来查找模块，模块解析速度更快。
磁盘空间节省: 依赖以压缩文件形式存储，避免了重复存储和文件夹深度嵌套问题。
提高安全性: 更明确的依赖和版本管理，有助于防止隐式依赖和“幻影”依赖。
声明性更强: 所有的依赖和版本信息都集中在 .pnp.js 文件中，易于管理和审查。
使用 PnP
要在 Yarn 中启用 PnP，可以在 .yarnrc.yml 文件中设置 nodeLinker 选项为 pnp:

yaml
nodeLinker: pnp
然后，你需要重新安装依赖：

sh
yarn install
常见问题和解决方案
兼容性问题: 并非所有的工具和依赖包对 PnP 友好，可能会出现需要调整的情况。 yarn 提供了一些工具和配置选项来帮助解决这些问题。
传统工具的适配: 对于不兼容 PnP 的模块或工具，可以使用 yarn unplug 命令将其解压到 node_modules 目录来解决问题。
例子
假设一个简单的 .yarnrc.yml 配置：

yaml
nodeLinker: pnp
enableGlobalCache: true
enableImmutableCache: true
通过这样配置，你便启用了 PnP 功能，同时使用全局缓存和不可变缓存特性，从而提升项目的依赖管理效率。

总结来说，PnP 是 Yarn 提供的一项强大功能，可以显著提升依赖管理的性能和安全性，但在启用时需考虑兼容性问题。