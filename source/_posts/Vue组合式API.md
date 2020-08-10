---
title: Vue组合式API
date: 2020-05-21 11:58:33
tags:
    - Vue杂谈
    - 工作经验总结系列
---
> 使用场景：抽取的公共项目写example的时候会用


#### 引用方式
```
dependencies:
    "@vue/composition-api" "^0.5.0"
```
<pre>
"@vue/composition-api@^0.5.0":
  version "0.5.0"
  resolved "http://XXX/repository/npmjs.org/@vue/composition-api/-/composition-api-0.5.0.tgz#2dbaa02a5d1f5d0d407d53d5529fe444aa8362f3"
  integrity sha1-LbqgKl0fXQ1AfVPVUp/kRKqDYvM=
  dependencies:
    tslib "^1.9.3"
</pre>
```
import Vue from 'vue'
import VueCompositionAPI from '@vue/composition-api'

Vue.use(VueCompositionAPI)
// 使用 API
import { ref, reactive } from '@vue/composition-api'
```
