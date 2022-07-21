---
title: ansible
date: 2021-06-14 16:11:25
tags:
---
> 官网指路：https://www.ansible.com/

Devops平台: 解决一线研发交付团队的实际问题
Gitlab/Github : 解决配置管理问题 - 代码管理平台
Jenkins： 解决集成打包问题 - 集成与编译系统

Ansible —— 自动化运维管理工具,angentless(不需要在目标机器安装agent进程)

（chef,puppet,salt）

- 安装
```
sudo pip install Ansible
```
```
yum install python-pip
python -m pip --version
pip install --upgrade pip
```

### 运维老师对sudo版本升级


### Fedora - 36
```
Ansible is updated to Ansible 5. Playbooks may behave differently. Users are encouraged to read the upstream Porting Guide for further information.

Additionally, Ansible is now shipped as multiple packages: ansible-core (the engine) and a curated set of Ansible collections (ansible-collection-*). The command dnf install ansible will install ansible-core as well as the Ansible collections included in the upstream Ansible releases. You can also choose to dnf install ansible-core and then manually install collections from the individual packages or with the ansible-galaxy command.
```