---
title: corepack
date: 2024-04-02 13:43:13
tags:
---
- https://pnpm.io/zh/installation
```
使用 Corepack 安装
从 v16.13 开始，Node.js 发布了 Corepack 来管理包管理器。 这是一项实验性功能，因此您需要通过运行如下脚本来启用它：

提示
如果您已使用pnpm env安装Node.js，则Corepack不会被安装在您的系统上，您需要单独安装它。 见#4029。

corepack enable pnpm

如果您已经使用Homebrew安装了Node.js，您需要单独安装Corepack：

brew install corepack

这会自动将pnpm安装在您的系统上。

你可以通过下列命令固定项目所用的 pnpm 版本：

corepack use pnpm@latest

这会添加一个 packageManager 字段到您本地的 package.json，指示 Corepack 始终在该项目上使用特定的版本。 如果您想要可复现性，这可能很有用，因为所有使用 Corepack 的开发人员都将使用与您相同的版本。 当一个新版本的 pnpm 发布时，您可以重新运行上述命令。
```

Corepack is an experimental tool to help with managing versions of your package managers. It exposes binary proxies for each supported package manager that, when called, will identify whatever package manager is configured for the current project, download it if needed, and finally run it.
Corepack 是一个实验性工具，可帮助管理包管理器的版本。它为每个受支持的包管理器公开二进制代理，当调用这些代理时，将识别为当前项目配置的任何包管理器，根据需要下载它，最后运行它。

Despite Corepack being distributed with default installs of Node.js, the package managers managed by Corepack are not part of the Node.js distribution and:
尽管 Corepack 的默认安装量为 Node.js，但 Corepack 管理的包管理器不是 Node.js 发行版的一部分，并且：

Upon first use, Corepack downloads the latest version from the network.
首次使用时，Corepack 会从网络下载最新版本。
Any required updates (related to security vulnerabilities or otherwise) are out of scope of the Node.js project. If necessary end users must figure out how to update on their own.
任何必需的更新（与安全漏洞或其他相关）都超出了 Node.js 项目的范围。如有必要，最终用户必须弄清楚如何自行更新。
This feature simplifies two core workflows:
此功能简化了两个核心工作流：

It eases new contributor onboarding, since they won't have to follow system-specific installation processes anymore just to have the package manager you want them to.
它简化了新贡献者的入职培训，因为他们不必再遵循特定于系统的安装过程，只是为了拥有您希望他们使用的包管理器。

It allows you to ensure that everyone in your team will use exactly the package manager version you intend them to, without them having to manually synchronize it each time you need to make an update.
它允许你确保团队中的每个人都将完全使用你希望他们使用的包管理器版本，而不必在每次需要更新时手动同步它。