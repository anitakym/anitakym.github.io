---
title: ssh配置
date: 2021-05-05 14:23:59
tags:
---
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