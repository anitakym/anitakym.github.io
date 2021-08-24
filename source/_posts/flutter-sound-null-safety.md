---
title: flutter-sound-null-safety
date: 2021-08-24 10:44:15
tags:
---

### 英文贴士

sound 这里指完全的，彻底的； （adj,只能用在名词前）

### sound null safety 迁移

- dart pub get // 更新 pub
- dart pub outdated --mode=null-safety // 展示没有升级到 null-safety 的依赖
- 修改依赖库的版本
- dart pub get // 更新 pub

#### 自动迁移

- dart migrate --apply-changes

#### 手动迁移

- dart migrate // 按提示操作
