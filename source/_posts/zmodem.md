---
title: zmodem
date: 2024-04-26 14:45:31
tags:
---
在SSH会话中，你可以使用Zmodem进行文件传输。Zmodem是一种错误检测和纠正软件协议，它可以用于在两台计算机之间高效地传输文件，比如使用SSH进行远程登陆的场景。

以下是使用步骤：

1. 确保你已经在两台计算机上安装了`lrzsz`程序，这是Zmodem的一种实现。在大多数Unix和Linux发行版上，你可以使用包管理器来安装它。比如在Debian或Ubuntu上，你可以使用`apt-get install lrzsz`。在Fedora或CentOS上，你可以使用`yum install lrzsz`。

2. 在SSH进入远程服务器后，切换到你想要传输文件的目录，然后使用`rz`命令在远程服务器上启动Zmodem接收文件模式。

3. 接下来，在SSH客户端软件中选择`发送文件`，然后选择你想要传输的文件。完成后，Zmodem应该会自动开始传输文件。

对于发送文件到远程服务器，反向操作即可，使用`sz`命令发送文件。

注意: 以上步骤在使用Zmodem支持的SSH客户端软件方有效，例如SecureCRT和Xshell，对于不支持Zmodem的SSH客户端，例如PuTTY，这个方法可能无法使用。

当然，Zmodem是一种文件传输协议，它在1986年由Chuck Forsberg开发完成。

Zmodem是Ymodem的改进版，相比于Ymodem协议，Zmodem有如下的优点：

1. **错误恢复**：在文件传输过程中，如果发生错误，Zmodem可以中断和恢复传输，而不必从头开始传输文件。

2. **高效**：Zmodem包含了数据压缩和链接检验的功能，使用滑动窗口进行数据传输，减少了由于网络延迟导致的带宽浪费，从而提高了传输速度。

3. **功能强大**：Zmodem还可以保留文件的原始日期和权限设置，并支持大文件(超过1GB)的传输。

4. **兼容性**：Zmodem协议支持不同操作系统间的文件传输。

在Unix和Linux环境下，常常使用rz和sz命令进行Zmodem协议的文件传输，其中rz是接收文件的命令，sz是发送文件的命令。如果你在MacOS上使用的终端支持Zmodem协议，你便可以在不同设备之间便捷地传输文件。

注意，Zmodem是一种较为老旧的协议，在不同环境中的表现可能会受限，例如在高延迟、丢包率高的网络环境下，其性能可能不尽如人意。

在这种场景下，你有多种选择可以从你的 macOS 系统传输文件到 CentOS 8 服务器。下面是其中一些选项：

1. **SSH (Secure Shell) / SCP (Secure Copy)：** SCP 是基于 SSH 协议进行安全的远程文件传输，大多数 Unix/Linux 系统和 macOS 默认都安装了 SSH 和 SCP 工具。你可以使用 `scp` 命令来复制文件或目录。

   使用示例： `scp /path/to/local/file username@remote:/path/to/remote/directory`
   
2. **SFTP (SSH File Transfer Protocol)：** 和 SCP 类似，SFTP 也是基于 SSH，但是提供了更多高级功能，如恢复中断的传输、删除远程文件和创建远程目录等。

   使用示例： 首先输入 `sftp username@remote` 开启 sftp 会话，然后可以使用 `put` 和 `get` 命令进行文件上传和下载。
   
3. **rsync：** rsync 是另一种在 Unix/Linux 之间同步文件的工具，特别适合大文件和目录的复制。它可以通过 SSH 进行安全传输。

   使用示例： `rsync -avz /path/to/local/file username@remote:/path/to/remote/directory`
   
4. **Zmodem：** Zmodem 是一种错误检测和纠正协议，适合在噪音环境中传输文件。需要在两端都安装 lrzsz 工具。
   
   使用示例： 在 macOS 安装 lrzsz (`brew install lrzsz`)，SSH 登录到 CentOS 服务器后，使用 `sz` 命令发送文件，`rz` 命令接收文件。 

请注意每种方法都有其自身的优点和缺点。选择最佳的工具取决于你的特定需要，如传输大小、带宽、文件类型等。


### rsync-增量
rsync -avz ./homework-预发环境上的包/ ./homework-线上拉取的线上包/
