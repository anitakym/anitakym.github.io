---
title: vue-testing-jest
date: 2022-04-24 11:48:03
tags:
---
## reference
- https://github.com/alexjoverm/vue-testing-series
## jest
Jeff Morrison
减少测试一个项目所要花费的时间和认知负荷
TDD - test-driven development - 构建稳定可靠的库

#### 特点
- Facebook
- out of box
- assertion mock
- snap 测试
- Istanbul - coverage report
- 并行测试

#### snapshot
- https://github.com/facebook/jest/blob/main/packages/jest-core/src/lib/__tests__/logDebugMessages.test.ts


#### log

#### cross-env
Jest默认commonjs方式导入的
`npm i cross-env -D`
- 解决ESM不支持的问题，可以用这个，使用Jest最新的原生支持ESM的特性
- `"jtest": "cross-env NODE_OPTIONS=--experimental-vm-modules jest",`
- https://www.npmjs.com/package/cross-env

#### eslintrc.js
env - jest:true
- 让eslint识别jest框架定义的方法

#### 异步测试
- async/await
- 回掉函数
- 以上都支持


#### 覆盖率
- jest 默认执行项目目录下所有`.test.js`文件
- `"jtest": "cross-env NODE_OPTIONS=--experimental-vm-modules jest --coverage",`
- 第三方库方式载入的代码，不会被测试覆盖率检查，需要测试，就拉到本地测试（不走npm
## others

#### jasmine - 基于BDD
- behavior-driven development
- 行为驱动测试 - 通过用自然语言书写非程序员可读的测试用例
- observable
- reducer - 纯函数 - 好测试
- 一个命令行就可以生成spec - angular