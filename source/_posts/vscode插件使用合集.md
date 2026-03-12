---
title: vscode插件使用合集
date: 2020-08-06 15:37:05
tags:
    - 工具篇
---
### 当扩展很慢的时候
- Developer：show running extensions (发现哪些导致慢)
- https://code.visualstudio.com/updates/v1_32#_bundling-extensions-with-webpack?wt.mc_id=devto-blog-jopapa  - 官方提供了打包功能
#### 写在前面
调出——显示所有命令（cmd + shift + P）
然后搜索 code
选择 install code command in path 
这样就可以在shell中直接通过code xxx 调起vscode 来


#### vscode常用快捷键：
- 显示所有命令（cmd + shift + P）
- 转到文件（cmd + P）
- 在文件中查找（cmd + shift + F）
- 开始调试（F5）

#### Plugin: vscode-faker
使用场景:
目标，生成一行行的名字如下
```
export default `
Abbott
Turner
Kutch
Reichert
Funk
Mante
Hammes
Howell
`.trim().split(/\s+/g)
```
用这些名字，生成一个name的数组，那么，怎么生成一行一个名字呢？

<strong>vscode-faker</strong> + 多行选中功能

1. 利用多行选择和faker
2. alt+shift (先点击第一行，按完快捷键后，再点击最后一行)
3. 再cmd+shift+p调出faker，选中要生成的类型即可

####  Plugin: open in browser

我的家里电脑的chrome浏览器之前点击open in browser 一直没有反应，升级了之后就好了（但是也是只在没有打开过浏览器页面的情况下生效

那么open in browser or view in browser 的原理是什么呢？ 为什么会产生我家里电脑那种情况呢？

插件评级星星边上有repository，可以通过这个点到github里面去看他们具体的实现
```
const opn = require('opn');

export const open = (path: string, browser: string = '') => {
  // const name = browser ? browser : standardizedBrowserName(defaultBrowser());
  // const name = standardizedBrowserName(browser);
  opn(path, { app: browser })
    .catch(_ => {
      vscode.window.showErrorMessage(`Open browser failed!! Please check if you have installed the browser ${browser} correctly!`);
    });
};
```
```
https://www.npmjs.com/package/opn //opn链接，现已更名open
```

PS: 一般情况下，我要打开静态资源，会起个静态资源服务，就OK了，http-server

#### svg viewer
可以看svg图片


#### koroFileHeader
团队注释规范，可以制定好规范，提供配置给团队成员使用


#### 插件推荐
https://github.com/varHarrie/varharrie.github.io/issues/10


如何本地调试 VSCode 插件
按 F5 (or Run->Start Debugging)，开一个带当前 extension 的 VSCode 窗口

## VS Code 扩展测试：Vitest + vscode-test（@vscode/test-electron）

目标与分工
- Vitest：测纯函数/工具模块（不需 VS Code 宿主）。
- @vscode/test-electron：在独立 VS Code 实例内跑“扩展级集成测试”（可访问 vscode API）。

安装（建议 TypeScript）
```bash
npm i -D vitest typescript ts-node @types/node @types/vscode @vscode/test-electron
```

目录建议
```
src/
  extension.ts
  test/
    runTest.ts            # 启动 VS Code 扩展测试宿主
    suite/extension.test.ts  # 集成测试（vscode API）
test/
  unit/sum.test.ts        # Vitest 单元测试
```

示例：Vitest 单元测试（无需 VS Code）
```ts
// filepath: test/unit/sum.test.ts
import { describe, it, expect } from 'vitest'
const sum = (a: number, b: number) => a + b

describe('sum', () => {
  it('adds', () => {
    expect(sum(1, 2)).toBe(3)
  })
})
```

示例：扩展集成测试（vscode-test）
```ts
// filepath: src/test/suite/extension.test.ts
import * as assert from 'assert'
import * as vscode from 'vscode'

suite('Extension Suite', () => {
  test('vscode API ok', async () => {
    const docs = await vscode.workspace.findFiles('**/*')
    assert.ok(Array.isArray(docs))
  })
})
```

示例：启动扩展测试（下载并启动专用 VS Code）
```ts
// filepath: src/test/runTest.ts
import * as path from 'path'
import { runTests } from '@vscode/test-electron'

async function main() {
  const extensionDevelopmentPath = path.resolve(__dirname, '../..')
  const extensionTestsPath = path.resolve(__dirname, './suite')
  await runTests({ extensionDevelopmentPath, extensionTestsPath })
}
main().catch(err => {
  console.error('Failed to run tests', err)
  process.exit(1)
})
```

package.json 脚本
```json
{
  "scripts": {
    "test": "vitest",
    "test:unit": "vitest run",
    "build": "tsc -p .",
    "test:ext": "ts-node src/test/runTest.ts"
  }
}
```

替代方案（更少胶水）
- vscode-test-cli：无需写 runTest.ts，直接 CLI 启动
```bash
npm i -D vscode-test-cli
npx vscode-test --extensionDevelopmentPath=. --extensionTestsPath=./out/test/suite
```

小贴士
- 集成测试前先编译（或用 ts-node/tsx 直接跑）。
- 将高风险/慢用例放集成测试，纯逻辑放 Vitest，缩短反馈链路。
- Web 扩展可用 @vscode/test-web；Electron 环境用 @vscode/test-electron。

### vscode-test
https://github.com/Microsoft/vscode-test
https://github.com/microsoft/vscode-test-cli