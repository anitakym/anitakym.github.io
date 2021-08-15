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