---
title: docker-node-k8s项目实践总结
date: 2021-04-03 12:21:24
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
####   Kubernetes
####   Kompose
### OCI (Non-Docker) Containers （OCI(非Docker)容器）
####   Buildah
####   Podman
### Wrapping Up (收尾工作)
####   Conclusion (结论)

PS：把材料放到github,也是因为文本材料的错误不可能完全无一点错误，所以放到github上，大家都可以提issue（问题），这样后续的人，就能方便查到了；而材料也能在这个过程中不断得完善; video课程收费，但是材料开源;


### 项目介绍


### 存在问题



### 做的优化



### 随便聊聊
之前看了阿里巴巴云原生的一篇访谈博文（https://juejin.cn/post/6951283312824418311）：
里面Nacos联合创始人做了一个类比：Nacos之于微服务的地位，就跟Etcd之于k8s的地位一样

