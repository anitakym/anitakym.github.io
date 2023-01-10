---
title: complete-intro-to-containers-study-notes
date: 2021-11-10 18:51:11
tags:
---
## 推荐学习资料:
一定要点开，完整而全面 —— 也是frontend masters上面的一门课
https://btholt.github.io/complete-intro-to-containers/

下面是简单翻译：
TABLE OF CONTENTS（目录）
### Welcome
####   Introduction
### Crafting Containers By Hand
#### What Are Containers? (什么是容器？)
#### chroot 隔离在chroot环境中，看不见彼此的文件
- chroot - run command or interactive shell with special root directory
  - 容器环境：安全性
- docker run -it --name docker-host --rm --privileged ubuntu:bionic
  - 注意拉取时候，如果报拉取错误，可以处理下代理配置
  - docker run意味着我们要在容器中运行一些命令，而-it意味着我们要使shell交互式（所以我们可以像普通终端一样使用它）
  - 执行完这个命令后：
  ```
  # 我们可以查下ubuntu的版本
  root@3595a31d9cad:/# cat /etc/issue
  mkdir /my-new-root
  cd /my-new-root
  echo "my super secret thing" >> /my-new-root/secret.txt

  mkdir /my-new-root/bin
  cp /bin/bash /bin/ls /my-new-root/bin/

  # ldd - print shared object dependencies,列出bash依赖的库，copy到我们新的环境
  ldd /bin/bash
  cp /lib/x86_64-linux-gnu/libtinfo.so.5 /lib/x86_64-linux-gnu/libdl.so.2 /lib/x86_64-linux-gnu/libc.so.6 /my-new-root/lib
  cp /lib64/ld-linux-x86-64.so.2 /my-new-root/lib64
  ldd /bin/ls
  cp /lib/x86_64-linux-gnu/libselinux.so.1 /lib/x86_64-linux-gnu/libpcre.so.3 /lib/x86_64-linux-gnu/libpthread.so.0 /my-new-root/lib

  chroot /my-new-root bash
  ls
  pwd
  cat secret.txt
  Ctrl + D #exit

  ```
####   Namespaces (命名空间) - 创建一个新的环境，它被隔离在系统中，有自己的PID、挂载（如存储和卷）和网络栈，避免容器间进程等彼此可见性
1. 我有一个大服务器，空间卖给几个人
2. 如果将用户限制在chroot的环境中，他们看不见彼此的文件，但是依然可以看到（or kill or hijack）所有的进程
3. 如果再给每个chroot环境提供不同的命名空间，他们就看不到对方的进程了
4. 刚刚说的是UTS（or UNIX Timesharing）命名空间；还有更多的命名空间可以帮助容器保持相互隔离
- 安全性的试验
```
# 在一个终端里面chroot到我们的环境 - terminal session 1
# 在另外一个终端
docker exec -it docker-host bash # terminal session 2

tail -f /my-new-root/secret.txt & # ts 2 在后台启动一个无限运行的进程
ps # 2
kill <PID you just copied> # 1 
```
我们可以从chroot环境中，kill掉tail进程，这说明我们不仅仅需要文件系统的隔离

因此，我们使用unshare来创建一个使用namespace来隔离的chroot环境
```
exit # 从之前的chroot环境

# 安装 debootstrap
apt-get update -y
apt-get install debootstrap -y
debootstrap --variant=minbase bionic /better-root

# 进入新的命名空间和chroot环境
unshare --mount --uts --ipc --net --pid --fork --user --map-root-user chroot /better-root bash # this also chroot's for us
mount -t proc none /proc # process namespace
mount -t sysfs none /sys # filesystem
mount -t tmpfs none /tmp # filesystem
```
这将创建一个新的环境，它被隔离在系统中，有自己的PID、挂载（如存储和卷）和网络栈。现在，我们看不到任何进程了。
PIDs + mounts(like storage and volumes, network stack)

可以再试试刚刚的安全试验

我们可以用namespace来限制容器相互干扰的能力（也可以试试其他的namespace）

####   cgroups - 物理资源隔离限制
我们还有一个问题，每个隔离的环境都可以访问服务器所有的资源。环境之间的物理组件没有做隔离。
Google在建立基础设施的时候，也遇到了这个问题，于是提出了cgroup;这个隔离环境只能得到这么多的CPU，内存，一旦用完了，就不会再得到更多了。
- Linux Cgroups - Linux Control Group - 限制一个进程组能够使用的资源上限（CPU，内存，磁盘，网络带宽）
```
# 在unshare'd环境之外，我们先安装下需要的工具
apt-get install -y cgroup-tools htop

# 创建新的 cgroups
cgcreate -g cpu,memory,blkio,devices,freezer:/sandbox

# 将我们的 unshare'd 环境添加到 cgroup 中
ps aux # 拿到 紧跟在 the unshare 环境之后的 the bash PID 
cgclassify -g cpu,memory,blkio,devices,freezer:sandbox <PID>

# 列出与沙盒cpu组相关的任务，我们可以看到上面的PID
cat /sys/fs/cgroup/cpu/sandbox/tasks

# 看下沙盒cpu组的cpu份额，这个数字决定了竞争资源之间的优先级，越高的优先级就越高
cat /sys/fs/cgroup/cpu/sandbox/cpu.shares

# 如果需要的话，kill所有沙盒的进程
# kill -9 $(cat /sys/fs/cgroup/cpu/sandbox/tasks)

# 对于多核系统，将使用率限制在5%
cgset -r cpu.cfs_period_us=100000 -r cpu.cfs_quota_us=$[ 5000 * $(getconf _NPROCESSORS_ONLN) ] sandbox

# 设置一个80M的限制
cgset -r memory.limit_in_bytes=80M sandbox
# 获取cgroup使用的内存统计信息
cgget -r memory.stat sandbox

# 在终端会话 #2 中，在unshare 环境之外
htop # 将允许我们通过一个漂亮的可视化工具查看资源使用情况

# 在终端会话 #2 中，在unshare 环境中
yes > /dev/null 
# 这将迅速消耗核心的CPU功率
# 注意它只占用5%的CPU，就像我们设定的那样
# 如果你愿意，可以运行上面的docker exec来获得第三个会话，看看上面的命令是否占用了100%的可用资源
# CTRL+C随时停止上述操作

# 在终端会话#1中，在unshared的环境中
yes | tr \\n x | head -c 1048576000 | grep n # 这将加速消耗 ~1GB 的内存

# 注意在 htop 中，由于我们的 cgroup，它将保持内存接近 80MB
# 如上所述，用第三个终端连接，看看上面的命令在cgroup之外的工作情况
```
所以，尽管这是最基本意义上的容器，但我们还没有触及更多高级的话题，比如网络、部署、绑定，或者其他Docker为我们提供的服务。但现在你已经知道在最基本的层面上，容器是什么，它做什么，以及我们如何自己实现这些。
### Docker
####   Getting Set Up with Docker (使用Docker进行设置)
####   Docker Images without Docker
####   Docker Images with Docker
####   Node.js on Docker
####   Tags (标签)
####   Docker CLI
### The Dockerfile
####   Intro to Dockerfiles (Dockerfiles介绍)
####   Build a Node.js App (构建一个Node.js应用)
####   A More Complicated Node.js App (一个更复杂的Node.js应用)
####   A Note on EXPOSE (关于EXPOSE的说明)
####   Layers
### Making Tiny Containers
####   Alpine Linux
####   Making Our Own Alpine Node.js Container (制作我们自己的Alpine Node.js容器)
####   Multi Stage Builds
####   Static Assets Project
### Features in Docker
####   Bind Mounts
####   Volumes
####   Using Containers for your Dev Environment (在开发环境中使用容器)
####   Dev Containers with Visual Studio Code
####   Networking with Docker
### Multi Container Projects (多容器项目)
####   Docker Compose
docker-compose up -d=>在后台运行
####   Kubernetes
####   Kompose
### OCI (Non-Docker) Containers （OCI(非Docker)容器）
####   Buildah
####   Podman
### Wrapping Up (收尾工作)
####   Conclusion (结论)

PS：把材料放到github,也是因为文本材料的错误不可能完全无一点错误，所以放到github上，大家都可以提issue（问题），这样后续的人，就能方便查到了；而材料也能在这个过程中不断得完善; video课程收费，但是材料开源;


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

- 容器技术的核心 - 通过约束和修改进程的动态表现，从而为其创造出一个边界
- 在Linux内核中，很多资源和对象是不能被namespace化的，比如时间