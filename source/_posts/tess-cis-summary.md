---
title: tess-cis-summary
date: 2021-11-17 13:59:53
tags:
---
> Test and Error Support System - Continous Integration System
 
> 持续集成组搭建的

### Concept
持续构建系统 - 代码编译 ｜ 静态扫描 ｜ 制品打包 ｜ 环境发布 ｜ 自动化测试
质量管理工作平台 - 质量报告 ｜ 选择上线制品 ｜ 提上线单 （测试人员）

#### 流程图

项目/子项目 => 拉取代码 => 代码编译 => 二进制包｜docker镜像｜静态扫描（并行） => 开发｜测试｜预发环境（K8s|虚拟机） => 接口测试｜压力测试｜安全扫描（质量卡点） => 二进制包｜测试报告｜服务信息 （申请上线）=> 上线

#### 项目管理
集团那边项目管理是走这个的，项目管理无外乎项目信息的维护，人员权限的配置，服务器资源的管理，子项目的管理，操作记录等；
我们这边走禅道；

## 容器流水线
- 我们这边有node的服务走的是容器流水线
- 环境部署到kubernetes
- 编译打包的制瓶类型支持二进制（zip）包盒docker镜像，我们这边是docker镜像里面拷贝了个项目的zip包
```
# 流水线设置
源代码管理
编译管理（镜像,命令）
制品打包管理（文件或文件夹，部署目录、启动命令）
资源管理（服务端口、容器实例数、CPU、内存）
配置管理（代码拉取之后、编译之前对代码的配置文件进行更改）
流水线任务开关（静态扫描等进行开启或关闭）
质量卡点管理（配置TESS-ATS、压力测试等）
```

## 登录容器
一般是到跳板机上，然后```kubectl```登录方式；```kubectl get pods -n NAMESPACE |grep 子项目名``` ```kubectl exec -it 容器名称 bash -n NAMESAPCE```

### Q环境
Q环境一般是指Quality Assurance环境， 即质保环境，也称为测试环境。开发人员在完成每个项目或功能点的开发工作后，会把代码部署到Q环境中，然后由专门的QA团队（质量保证团队）进行全面、系统的测试，以确保软件的质量和功能满足设定的需求。

软件在Q环境中，需要接受功能测试、性能测试、安全测试、兼容性测试等多方面的测试。测试人员会按照测试用例进行操作，如发现问题，就会录入bug，让开发团队在后续的版本中进行修复。所以，Q环境是从开发环境到生产环境的重要过渡，也是保证软件质量的关键步骤。

在一些组织中，还存在与Q环境类似的环境，如UAT环境（用户接受测试环境），PRE环境（预上线环境）等。不同环境的目的在于模拟可能的软件使用场景，尽可能发现和解决软件存在的问题，使其在上线后能正常运行，提供良好的用户体验。