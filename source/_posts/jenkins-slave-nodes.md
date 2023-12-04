---
title: jenkins-slave-nodes
date: 2023-12-04 14:28:22
tags:
---
- 增加slave节点，用于构建
- 场景 - nodejs18对于centos8的需求
- Jenkins在centos7的机器上

- manage jenkins
- manage nodes and clouds
- 新建节点

- 用标签或者节点名字都能匹配，标签可以起个简洁的
- only build jobs with label expressions matching this node
- 启动方式（launch agents via ssh - 需要安装ssh插件 ssh build agents）