---
title: chromium
date: 2021-08-13 16:01:33
tags:
---

https://chromium.googlesource.com/chromium/src/+/refs/heads/main/docs/mac_build_instructions.md#Get-the-code

#### history

https://github.com/chromium/chromium/blob/d7da0240cae77824d1eda25745c4022757499131/chrome/browser/extensions/api/history/history_api.h

https://github.com/chromium/chromium/blob/d7da0240ca/components/history/core/browser/browsing_history_service.cc

- Chromium - 多进程架构
- ipc
## Browser - 1


## Renderer     - n




#### electron
node.js和chromiums整合
- node.js的事件循环基于libuv
- chromium的事件循环基于message bump
- chromium集成到node.js：用libuv实现messagebump(nw)
- nodejs集成到Chromium：electron - shelley Vohr - JSHeroes2019
```
A event happeds in node   |a   Electron Main Thread   |b   Chromium MessageLoop
  |a    Electron's main thread is notified via the same fd as libuv
  |b    Electron tells Chromium's MessageLopp to clear libuv events
```

- electron-internals-node-integration(electronjs.org)
- Electron: The Event Loop Tightrope - Shelley Vohr | JSHeroes 2019 - ytb - JS/Heroes
- shell/common/node_bindings.cc

### bugs
- https://bugs.chromium.org/p/chromium/issues/list