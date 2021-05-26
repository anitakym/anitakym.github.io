---
title: gitlab集成钉钉
date: 2021-05-26 14:29:46
tags:
---
- 利用webhook

- 目标：评审comment，merge request，push tag的信息能通知到钉钉群里

- 方法：

1. 钉钉群：
群主在群设置里面，选择智能群助手，机器人管理里面新增gitlab机器人，然后复制出webhook的地址

2. gitlab:
在gitlab项目的settings里面，选择intergations,URL即为钉钉里面复制出来的地址，在trigger里面选择需要的触发点，点击 “add webhook”即可

Tips:
1. 如果想要进一步加强控制，可以起个服务，做控制和中转处理
