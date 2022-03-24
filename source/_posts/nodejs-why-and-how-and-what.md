---
title: nodejs-why-and-how-and-what
date: 2022-01-29 21:52:08
tags:
---

- 性能，并发性，可用性，可靠性，可扩展性
- 从开始设计，用于构建实时和并发系统
- 发展，改进中





## basic

#### process
```
当 Node.js 进程收到信号时，则将触发信号事件。 
Linux supports the standard signals listed below.  The second
       column of the table indicates which standard (if any) specified
       the signal: "P1990" indicates that the signal is described in the
       original POSIX.1-1990 standard; "P2001" indicates that the signal
       was added in SUSv2 and POSIX.1-2001.
       
process.on('SIGINT', () => {
  console.log('Received SIGINT. Press Control-D to exit.');
});

```
- https://man7.org/linux/man-pages/man7/signal.7.html -   SIGINT-P1990-Term-Interrupt from keyboard

```
Windows 不支持信号，因此没有等价的使用信号来终止，但 Node.js 提供了一些对 process.kill() 和 subprocess.kill() 的模拟：

发送 SIGINT、SIGTERM、和 SIGKILL 会导致目标进程无条件的终止，之后子进程会报告进程被信号终止。
发送信号 0 可以作为独立于平台的方式来测试进程是否存在。
```










## 其他语言
### golang
- coroutines
### erlang
- 抢占式调度


## Tools
#### volta - The Hassle-Free JavaScript Tool Manager
- https://volta.sh/
