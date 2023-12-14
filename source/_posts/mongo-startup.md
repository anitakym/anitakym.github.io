---
title: mongo-startup
date: 2023-12-06 14:33:13
tags:
---
### Mongosh
MongoDB Shell(Mongosh)是MongoDB的标准交互式JavaScript接口。直到MongoDB 4.2，标准的shell是mongo。在MongoDB 4.4中，Mongosh是一种新的命令行接口，用来代替老的mongo shell。这是因为Mongosh比起老的mongo shell有更多的现代化的交互特性。 

然而，MongoDB 4.4是在Mongosh正式发布之前就发布的。因此，MongoDB 4.4及其之前的版本的安装包中并不包含Mongosh，因为在那个时候Mongosh就还未开发完。如果你想在MongoDB 4.4或之前的版本中使用Mongosh，你需要自己去下载和安装。


### Artifactory
Artifactory是JFrog公司开发的一个强大的二进制包管理工具，支持各种主流的包管理系统，包括Java，Python，npm，npm，Maven，Gradle，NuGet，Ruby，YUM，Debian等。Artifactory可以帮助开发者和DevOps工程师存储、组织、管理（如访问控制、版本管理），以及跟踪他们的代码，减少构建和发布流程中的复杂性。

Artifactory主要包含以下特性：

1. 强大的二进制包管理能力：无论你是在本地还是在云端都可以管理和跟踪你的二进制包。
2. 强大的集成能力：与主流的CI/CD工具，像Jenkins，Bamboo，TeamCity，和Docker等等做了深度的集成。
3. 安全和访问控制：可以为你的仓库，包和元数据设置权限来保证你的代码的安全。
4. 版本管理：可以管理和跟踪你的包的版本，确保你总能找到你需要的版本。
5. 多仓库管理：Artifactory允许你为你的包设置不同的仓库，可以帮助你更好地组织你的包。

### prune
docker system prune
docker system prune -a

### 端口映射
如果在Docker容器中运行的应用程序需要通过网络进行交互，那么端口映射是必须的。如果没有进行端口映射，会遇到以下问题：
1. 外部访问：如果没有进行端口映射，那么外部设备（包括运行 Docker 的宿主机）无法通过网络访问到容器中的应用。这是因为 Docker 容器有自己的网络命名空间，对外界默认是隔离的。
2. 通信隔离：另外，如果多个容器之间需要进行通信，如果没有正确的端口映射，也可能导致相互之间无法通信。
3. 服务使用限制：对于某些需要阿尔特端口（如HTTP服务的80端口， HTTPS服务的443端口）的服务，如果你没有进行端口映射，可能就无法正常提供服务。


### mongo compass
- 可视化，及时更新客户端，关注release