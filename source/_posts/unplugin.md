<!--
 * @Author: yimin kuang
 * @Date: 2024-08-07 11:29:10
 * @LastEditors: yimin kuang
 * @LastEditTime: 2024-08-07 11:30:39
 * @Description: 描述信息
-->
---
title: unplugin
date: 2024-08-07 11:29:10
tags:
---

### unplugin
https://unplugin.unjs.io/guide/
Unplugin是一个用于创建通用插件的工具库。它可以帮助开发者编写一次插件，然后在多个构建工具（如Vite、Rollup、Webpack等）中使用。这样可以避免为每个构建工具编写和维护不同的插件版本，从而节省开发和维护成本。

Unplugin提供了一套统一的API，开发者可以使用这套API来编写插件。然后，Unplugin会根据当前的构建工具自动选择和调用相应的插件接口。这样，开发者就可以专注于插件的功能实现，而不需要关心不同构建工具的插件接口差异。

Unplugin还提供了一些额外的功能，如自动处理文件路径和模块解析，以及提供一些常用的工具函数等。这些功能可以进一步简化插件的开发过程。

- https://github.com/umijs/mako/issues/1238
RFC：基于 unplugin 设计插件层的 API #1238
