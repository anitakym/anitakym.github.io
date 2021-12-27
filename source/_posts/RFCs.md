---
title: RFCs
date: 2021-12-24 09:48:12
tags:
---
## Vuejs
- https://github.com/vuejs/rfcs

## Reactjs
- https://github.com/reactjs/rfcs

## Rust
- https://github.com/rust-lang/rfcs

## Basic
### What is an RFC?
```
The "RFC" (request for comments) process is intended to provide a consistent and controlled path for new features to enter the framework.

Many changes, including bug fixes and documentation improvements can be implemented and reviewed via the normal GitHub pull request workflow.

Some changes though are "substantial", and we ask that these be put through a bit of a design process and produce a consensus among the Vue core team and the community.
```
- Request for comments
- 目的是为新feature进入框架提供一个一致，可控的路径
- pull request 能搞定很多changes，bug fixes等，但是一些 “substantial” - 实质性的改变，这些是需要经过一定的设计过程，并能在Vue的核心团队和社区中达成共识的
- Substantial的判断标准
```
A new feature that creates new API surface area
Changing the semantics or behavior of an existing API
The removal of features that are already shipped as part of the release channel.
The introduction of new idiomatic usage or conventions, even if they do not include code changes to Vue itself.
创造新的API surface area 的feature
改变现有API的语义或行为
移除已经作为发布的一部分的功能
引入新的习惯用法或惯例，即使它们不包括对Vue本身的代码修改
```

### The RFC life-cycle
```
An RFC goes through the following stages:

Pending: when the RFC is submitted as a PR.
Active: when an RFC PR is merged and undergoing implementation.
Landed: when an RFC's proposed changes are shipped in an actual release.
Rejected: when an RFC PR is closed without being merged.
```
- 四个阶段
- Pending ｜ Active ｜ Landed ｜ Rejected


### and ...
- 具体的流程，工作方式，项目清单，都可见具体对应项目的readme文档