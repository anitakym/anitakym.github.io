---
title: easy-monitor-3-接入
date: 2021-11-23 15:34:01
tags:
---
### Doc
- https://www.yuque.com/hyj1991/easy-monitor/deployment



### pre
- https://stackoverflow.com/questions/50093144/mysql-8-0-client-does-not-support-authentication-protocol-requested-by-server
```
ALTER USER 'root' IDENTIFIED WITH mysql_native_password BY 'password';
```


## 服务部署
```
wget https://repo.mysql.com//mysql80-community-release-el8-1.noarch.rpm


mysql:

yum -y install nodejs
npm install -g n
yum install git -y

# 项目可以fork一下，把config.prod.js加一下，推上去
git clone https://github.com/X-Profiler/xprofiler-console
git clone https://github.com/X-Profiler/xtransit-manager
git clone https://github.com/X-Profiler/xtransit-server

wget https://repo.mysql.com//mysql80-community-release-el8-1.noarch.rpm
rpm -ivh mysql80-community-release-el8-1.noarch.rpm
yum install mysql-server

https://dev.mysql.com/doc/refman/8.0/en/linux-installation-yum-repo.html

service mysqld restart

grep 'temporary password' /var/log/mysqld.log
mysql -uroot -p
alter user 'root'@'localhost' identified by 'xxxxxxxxx';

根据centos是7还是8安装对应的mysql,如80的安装在centos7上面就会出现问题

# /usr/bin/mysqladmin -u root password 'xxxx'
mysql -h localhost -u root -p
> create database xprofiler_logs;
> create database xprofiler_console;

cd xtrainsit-console/db
mysql -uroot -pxxxxxxxxx; -h127.0.0.1 -D 'xprofiler_console' < ./init.sql

cd xtrainsit-manager/db
mysql -uroot -pxxxxxxxxx -h127.0.0.1 -D 'xprofiler_logs' < ./init.sql
mysql -uroot -pxxxxxxxxx -h127.0.0.1 -D 'xprofiler_logs' < ./date.sql



redis

wget http://download.redis.io/releases/redis-5.0.8.tar.gz
tar -xvf redis-5.0.8.tar.gz
mv redis-5.0.8 /usr/local
cd /usr/local/redis-5.0.8/
yum list gcc
yum list tcl
yum install gcc # 版本
yum install tcl # 版本
make MALLOC=libc
make test
cd src && make install
vim redis.conf # daemon yes
./src/redis-server ./redis.conf


nginx 增加域名
emconsole.xxx.cn
172.111.111.111 emconsole.xxx.cn

/usr/local/tengine/sbin/nginx -s reload
/usr/local/tengine/sbin/nginx -t 


进入到gitlab各个项目下面，npm start

```

## prometheus
- 我们这边机器的监控是运维团队基于prometheus做的
- 目前Prometheus是按照k8s集群部署的, 每一个K8s集群都由独立的Prometheus来监控, (Prometheus部署在当前集群中)
- https://prometheus.io/docs/introduction/overview/
- 各个node运行node_exporter供prometheus采集数据，运行consul客户端注册节点信息向consul服务端，prometheus server从consul服务端获取所有的node节点，通过prometheus-es-adapter将数据持久化到es。配置alertmanager告警规则触发告警，监控指标图表通过grafana来查看
- jdk	｜ go ｜node-exporter ｜ prometheus-es-adapter	｜prometheus ｜ alertmanager｜ consul ｜elasticsearch ｜ kibana ｜grafana	
- 基于Prometheus 和 thanos 进一步增加了异常检测机制.  基于机器学习对阈值进行动态检测


### 转储
```
connect ECONNREFUSED 127.0.0.1:8443, POST http://127.0.0.1:8443/xapi/upload_from_xtransit?fileId=4&fileType=heapsnapshot&nonce=74904800742&timestamp=1646389590491&signature=a331a7a4fe28cdd275bfa0df3d937d9e4ca40c6a -1 (connected: false, keepalive socket: false, socketHandledRequests: 1, socketHandledResponses: 0) headers: {}
```

- config.xprofilerConsole = 'xxx';
- 这部分会提供给应用端，在调用转储的时候，应用端上传文件时候会请求 
```
  const url = `${server}/xapi/upload_from_xtransit?${qs.stringify({ fileId, fileType, nonce, timestamp, signature })}`;
```
- 这个里面的server，就从xprofilerConsole来，所以正式环境部署的时候，要给到能连通的url
- 分析策略，看给的各个应用服务的流程图，分析原因

### log_dir
性能分析文件会比较大，尽量不要放在会太影响memory的位置


### 一次内存泄漏问题排查

- 基于puppeteer的一个转svg的node服务
- 做压力测的时候，间隔时间gc,gc之后内存会往上涨
- 借助easy-monitor3, 堆快照，发现TCP -> Socket -> WebSocket 是泄漏点
- Search具体的，发现是WS
- 在package-lock里面搜ws ,发现被puppeteer依赖
- 这个时候查处理puppeteer部分的代码，发现有代码处理逻辑上，会错误的建立connect（对API使用有问题）
- 让处理了下这部分代码，解决问题


### docker + k8s
- https://www.yuque.com/hyj1991/easy-monitor/advance_docker

### 同类产品
NearForm 是一家总部位于爱尔兰的软件开发公司，他们专注于构建高性能、可扩展的 Node.js 和 JavaScript 应用程序。Clinic 是 NearForm 提供的一套开源工具，从多个角度帮助开发者识别和解决 Node.js 应用程序中的性能问题。该工具包括以下三个主要组件：

1. Clinic Doctor：此工具可帮助诊断应用程序中的常见性能问题，例如内存泄漏、CPU 泄漏或事件循环拥堵。通过可视化指标，Clinic Doctor 可以给出关于如何提高性能的建议。

2. Clinic BubbleProf：BubbleProf 是一种可视化数据流的工具，它可以帮助开发者了解应用程序中不同操作之间的关系。通过观察这些关系，开发者可以更容易地找到性能瓶颈和优化点。

3. Clinic Flame：Flame 是一个 CPU 火焰图分析器，它可以帮助开发者识别应用程序中的热点代码。它使用堆栈跟踪和定时器事件来显示哪些函数和操作占用了 CPU 的时间。

要使用这些工具，你需要在项目中安装 Clinic 包，然后运行相应的 Clinic 命令。例如，使用 Clinic Doctor 对应用程序进行诊断：

```
npm install -g clinic
clinic doctor -- node your-application.js
```

有关更多教程和示例，请访问 NearForm Clinic 的文档：https://clinicjs.org/

这些工具可以帮助你改进 Node.js 应用程序的性能，从而提供更好的用户体验。