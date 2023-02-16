---
title: vitest-summary
date: 2023-02-16 10:40:50
tags:
---
- https://github.com/vitest-dev/vitest/blob/main/examples/vue/vitest.config.ts

```
import { defineConfig } from 'vite'
import Vue from '@vitejs/plugin-vue'

export default defineConfig({
  plugins: [
    Vue(),
  ],
  test: {
    globals: true,
    environment: 'jsdom',
  },
})
```
处理需要操作DOM的环境

- https://cn.vitest.dev/guide/