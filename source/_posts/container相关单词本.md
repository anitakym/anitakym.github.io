---
title: container相关单词本
date: 2021-04-03 12:37:59
tags:
---
翻译内容笔记来自于下面开源链接：
https://btholt.github.io/complete-intro-to-containers/

### words notes:
#### intro
- Course Objective 课程目标
- The objective of this course is demystify what containers are  本课程的目的是解开什么是容器的神秘面纱
- demystify 使明白易懂 ｜diˈmɪstəˌfaɪ｜
- and now it's not just a tool for ops, it's a tool for developers 现在它不仅仅是运维的工具，也是开发人员的工具
- on a regular basis 经常
- a developer demographic 开发者群体
- the code will be incidental to the concepts being taught 代码是次要的
- incidental 1.次要的 2.不可避免的，伴随而来的 3.附带的
- to be incidental to sth 伴随某事物而来
- a very basic grasp of 非常基本的掌握
- be your first exposure to 第一次接触
- For set up instructions, refer here 关于设置说明，请参考这里
- File Issues 提交问题
- Previous to that 在此之前
- I love to teach. It's a challenging task that forces you to peel back all the knowledge you've gained so you can approach someone who lacks the same experience and terminology you have. It forces you to take amorphous(shapeless,confused) concepts floating in your brain and crystalize them into solid concepts that you can describe. It forces you to acknowledge(admit) your gaps(空白，空缺，欠缺) in knowledge because you'll begin to question things you know others will question. For me to ever master a concept, I have to teach it to someone else.
- incentive 激励

#### what are containers
- I was very intimidated by the concept of what containers were 我对容器的概念感到非常恐惧
- super-versed in Linux and sysadmin type activties 超级精通Linux和系统管理员类型的人
- a few features of the Linux kernel duct-taped together 将Linux内核的一些功能duct-taped在一起
- Honestly, there's no single concept of a "container": it's just using a few features of Linux together to achieve isolation. That's it. 说实话，"容器 "并没有一个单一的概念：它只是把Linux的几个功能用在一起实现隔离。仅此而已。
- assume wizardry(skill) with bash or zsh 
-  "bare metal" 裸机 
-  This is great if you're extremely performance sensitive and you have ample and competent staffing to take care of these servers.如果你对性能非常敏感，而且你有足够的和有能力的人员来照顾这些服务器，这是很好的。
-  Need to spin up another server
-  web traffic 网络流量
-  all the drivers connecting to the hardware 驱动程序连接到硬件
-  Virtual Machines 虚拟机
-  one beefy server 一个强大的服务器
-  lease a server from 租用了一台服务器
-   drop a fork bomb and devour（毁灭） all the resources
-   nefarious 恶毒的
-   a shared-tenant server 共享租户服务器
-   hum 嗯
-   All these above features come at the cost of a bit of performance. 以上这些功能都是以牺牲一点性能为代价的
-   Public Cloud 公有云
-   So, as alluded to above 因此，如上所述
-   manage all the software, networking, provisioning, updating, etc.管理所有这些服务器的软件、网络、配置、更新等。
-   We're still paying the cost of running a whole operating system in the cloud inside of a host operating system. It'd be nice if we could just run the code inside the host OS without the additional expenditure of guest OSs.
-   Containers 容器
-   divine 凭直觉发现，guess
-   As you may have divined, containers give us many of the security and resource-management features of VMs but without the cost of having to run a whole other operating system. It instead usings chroot, namespace, and cgroup to separate a group of processes from each other. 
-   flimsy (feeable,weak)
-   But I assure you a lot of very smart people have worked out the kinks and containers are the future of deploying code.但我向你保证，很多非常聪明的人已经解决了这些问题，容器是部署代码的未来。

