---
title: Chrome开发使用合集
date: 2020-03-12 15:44:46
tags:
    - 工具篇
---

#### Chrome基本原理
- 任何一个软件的帮助，里面可以搜索，快速找到某个功能，Chrome的帮助里面的搜索做的尤其的好（书签的搜索在里面也能搜）
- 窗口了 - 任务管理器 - Chrome
  - 按进程ID倒序，然后在浏览器里面打开新的标签页，观察任务管理器里面的变化
  - 从 A 标签页中打开 B 标签页（A,B同域下的），就会使用同一个渲染进程(用a标签或者window.open)，而分别打开这两个标签页，又会分别使用不同的渲染进程(打开新标签页，再输入网址；或者在A页面右键->在新标签页中打开链接)![](tags.png)
  - Chrome 浏览器会将浏览上下文组中属于同一站点的标签分配到同一个渲染进程中 (https://html.spec.whatwg.org/multipage/browsers.html#groupings-of-browsing-contexts)
  - rel= noopener a标签里面使用这个属性，可以切掉关联（引用关系）
  ```
  <a href="http://www.imaginingme.cn/img/avatar.jpeg" target="_blank" class="" rel="noopener">imaginingme</a>
  ```
  - 站点隔离: iframe —— 看是否属于同一站点，判断是否开新的渲染进程

  - 同站（same-site） 和同源（same-origin）—— 同源策略对同一站点的限制: A,B 标签页同站非同源，依然无法通过 opener 来操作父标签页中的 DOM —— 受同源策略的限制

#### chrome://chrome-urls/
里面有Chrome urls的合集
#### chrome canary


#### Disable cache
只有在开发者工具打开的时候，才会生效; 鼠标上去可以看到提示：disable cache（while devtools is open）


#### samesite问题
服务端利用cookies写入一些信息，
* 禁用samesite
<pre>
chrome://flags/
same-site(两个都改成disabled)
</pre>

#### preserve-log
![](preservelog.png)

#### chrome devtools protocol
https://chromedevtools.github.io/devtools-protocol/tot/Browser/
#### 写点小插件
