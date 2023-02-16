---
title: 异步I/O
date: 2023-02-16 10:44:05
tags:
---
## 基本概念
#### epoll
- https://en.wikipedia.org/wiki/Epoll
```
epoll is a Linux kernel system call for a scalable I/O event notification mechanism, first introduced in version 2.5.44 of the Linux kernel.[1] Its function is to monitor multiple file descriptors to see whether I/O is possible on any of them. It is meant to replace the older POSIX select(2) and poll(2) system calls, to achieve better performance in more demanding applications, where the number of watched file descriptors is large (unlike the older system calls, which operate in O(n) time, epoll operates in O(1) time[2]).

epoll is similar to FreeBSD's kqueue, in that it consists of a set of user-space functions, each taking a file descriptor argument denoting the configurable kernel object, against which they cooperatively operate. epoll uses a red–black tree (RB-tree) data structure to keep track of all file descriptors that are currently being monitored.[3]
```

#### 文件描述符

#### POSIX
- https://en.wikipedia.org/wiki/POSIX
```
The Portable Operating System Interface (POSIX) is a family of standards specified by the IEEE Computer Society for maintaining compatibility between operating systems.[1] 
```






## libuv
