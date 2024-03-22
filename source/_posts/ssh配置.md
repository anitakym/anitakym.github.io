---
title: ssh配置
date: 2021-05-05 14:23:59
tags:
---
## ssh连接问题
ssh之后连接会断，可以在服务器上面做配置：
```
vim /etc/ssh/sshd_config
ClientAliveInterval 60
ClientAliveCountMax 60

systemctl restart sshd
```

客户端配置：
```
vim /etc/ssh/ssh_config
ServerAliveInterval 60
```

TIPS:
systemctl | service 命令

华为云服务的帮助文档：
https://support.huaweicloud.com/trouble-ecs/ecs_trouble_0306.html

Init System

To run and manage your mongod process, you will be using your operating system’s built-in init system. Recent versions of Linux tend to use systemd (which uses the systemctl command), while older versions of Linux tend to use System V init (which uses the service command).

If you are unsure which init system your platform uses, run the following command:

ps --no-headers -o comm 1

Then select the appropriate tab below based on the result:

systemd - select the systemd (systemctl) tab below.
init - select the System V Init (service) tab below.

## 使用SSH连接到Github

### github文档指南
https://docs.github.com/cn/github/authenticating-to-github/connecting-to-github-with-ssh/about-ssh

这个文档强烈推荐，对于项目管理中的问题，给出了建议和最佳实践指南；可以当作解决问题的参考手册；


## screen和tmux实现会话恢复的机制



## 后台运行进程
`nohup`和`&`都是在Linux系统下用来在后台运行进程的工具，但他们的运行方式和具体功能有所不同。

**&**：

- `&` 是一个shell的内建命令，用来把命令放到后台执行。例如“command &”，该命令将在后台运行。
- 如果你在命令行中执行一个程序，然后你关闭该命令行，这个程序会立即停止。如果你用 `&` 把这个程序放入后台，这个程序会继续在你的控制领域之下运行，直到完成。

**nohup**：

- `nohup` 是一个非内建命令，它不依赖于shell，即使shell终结也可以继续执行。
- 如果你将一个程序用 `nohup` 和 `&` 运行，“nohup command &”，该命令就可以忽略所有来自shell的挂断（HUP）信号。即使你退出了shell，该命令也会在后台继续运行，直到完成。
- 它还会把标准输出和标准错误输出重定向到名为 nohup.out 的文件中，因此不会因为关闭Shell会话而丢失信息。

所以，`nohup`和`&`的主要区别在于，`nohup`保护进程不受Shell会话结束影响（甚至在用户注销之后也可以继续运行）,而 `&` 则只是简单地将进程放到后台运行。