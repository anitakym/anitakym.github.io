---
title: spectrum
date: 2019-11-21 15:52:20
tags:
    - websocket
    - 源码学习系列
---
> spectrum 是一个 online community 的开源项目，里面的技术栈可以参考习

#### 项目结构和技术栈
摘自官方README.md
<pre>
Codebase
Technologies
With the ground rules out of the way, let's talk about the coarse architecture of this mono repo:

Full-stack JavaScript: We use Node.js to power our servers, and React to power our frontend apps. Almost all of the code you'll touch in this codebase will be JavaScript.
Background Jobs: We leverage background jobs (powered by bull and Redis) a lot. These jobs are handled by a handful of small worker servers, each with its own purpose.
Here is a list of all the big technologies we use:

RethinkDB: Data storage
Redis: Background jobs and caching
GraphQL: API, powered by the entire Apollo toolchain
Flowtype: Type-safe JavaScript
PassportJS: Authentication
React: Frontend React app
Folder structure
spectrum/
├── api        # API server
├── athena     # Worker server (notifications and general processing)
├── chronos    # Worker server (cron jobs)
├── desktop    # desktop apps (build with electron)
├── docs
├── email-templates
├── hermes     # Worker server (email sending)
├── hyperion   # Rendering server
├── mercury    # Worker server (reputation)
├── public     # Public files used on the frontend
├── shared     # Shared JavaScript code
├── src        # Frontend SPA
└── vulcan     # Worker server (search indexing; syncing with Algolia)

</pre>