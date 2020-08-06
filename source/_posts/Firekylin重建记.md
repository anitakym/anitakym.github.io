---
title: Firekylin重建记
date: 2020-08-06 16:38:35
tags:
    - 安全篇
---

1. 博客因为mysql部分开放了远程访问，密码过于简单，导致被清库了；无库备份，或者sql执行语句的日志，所以之前的都没了。

2. 之后每篇博客都先notability里面写好，再上传firekylin的管理端

3. give me a lesson:安全很重要，备份很重要；自己搭的博客系统里面，不要使用自己的通用密码等信息，防止被攻击后，泄露重要信息；赶紧给自己的notability也给做了个备份，万一iCloud出问题了，可就真的是所有资料都没有了

4. 也借着这个机会，重新整理下博客，提高质量



> Continue----
1. 删除了mysql远程可登陆的账号后，还是又被清了库，推测被植入了程序，准备重装机器

#### 重装系统之后，安装基础的：

1. nodejs
```
curl --silent --location https://rpm.nodesource.com/setup_8.x | sudo bash -
yum -y install nodejs
```

然后
```npm i -g n```

n lts

2. pm2
```npm install pm2 -g```


3. mysql
```
wget http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm
rpm -ivh mysql-community-release-el7-5.noarch.rpm
yum install mysql-community-server -y
```

启动mysql服务：
```service mysqld restart```

设置root密码：
```/usr/bin/mysqladmin -u root password 'hahaGG89@Firekylin'```


4. 安装nginx:
yum install nginx -y


5. 安装git:
yum install git -y

走仓库版安装：
https://github.com/firekylin/firekylin/wiki/%E4%BB%93%E5%BA%93%E7%89%88%E5%AE%89%E8%A3%85

放弃本地所有提交：
git checkout .


#### firekylin 本身安全问题加强：url legacy && whatwg url
 （代码提交变更）


 #### firekylin startup代码解析
 启动完成后，在浏览器里输入 http://localhost:8360/ 即可访问首页填写配置信息
使用浏览器直接访问你的Blog地址即可看到 Firekylin 的安装程序。填入你的 MySQL 信息并设置好管理员账号后点击完成。

基于firekylin的代码对这个过程进行一个详细解析：



#### CSDN博客导出到firekylin的思路
看了看有64篇，因为想导出很久以前这个系列，保留发布时间，对内容做一些删减，所以找一个快速的方法来处理

1.比较老的文章，在文章管理点开是富文本编辑器
2.新一点的，在文章管理点开是md文件


拿到的东西
1.最优：直接处理了直接插库
2.拿到格式合适的一篇篇的添加文章（那还不如直接复制粘贴加审阅）

