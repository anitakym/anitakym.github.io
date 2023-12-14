---
title: docker-desktop-summary
date: 2023-12-14 21:02:41
tags:
---
windows - wsl

https://learn.microsoft.com/en-us/windows/wsl/install
默认是开启的
注意：
1. docker build -t aaa:ccc .
The command 'docker' could not be found in this WSL 2 distro.
We recommend to activate the WSL integration in Docker Desktop settings.
For details about using Docker Desktop with WSL 2, visit:
https://docs.docker.com/go/wsl2/

 wsl -l -v
 wsl.exe --setdefault Ubuntu-22.04


2. docker build -t aaa:ccc .
ERROR: permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/_ping": dial unix /var/run/docker.sock: connect: permission denied
sudo groupadd docker
sudo gpasswd -a $kkk docker
sudo gpasswd -a $USER docker
newgrp docker
(unix socket需要root权限访问，所以需要在子系统里面，将当前用户加到docker组里，docker守护进程启动的时候，会默认赋予名字为docker的用户组读写Unix socket的权限，因此只要创建docker用户组，并将当前用户加入到docker用户组中，那么当前用户就有权限访问Unix socket了，进而也就可以执行docker相关命令)
 