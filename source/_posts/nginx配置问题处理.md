---
title: nginx配置问题处理
date: 2020-08-03 16:46:32
tags:
    - nginx
---
> nginx（Engine X） 高性能的web服务器
  排名指路：https://w3techs.com/technologies/cross/web_server/ranking
  官网指路：http://nginx.org/en/

<pre>
轻量级： CPU，内存占用少（工作模式：进程池 + 单线程 => 消除了进程，线程切换的成本）
One master and several worker processes; worker processes run under an unprivileged user;
（在进程之上，master进程用来管理进程池，监控进程，自动恢复发生异常的worker，保持进程池的稳定和服务能力）
cite: https://time.geekbang.org/column/article/117492
</pre>
#### nginx - 作为web代理服务器 - 负载均衡，流量切换 - lua的脚本支持
```
- 对session和cookie的处理较弱
- 支持的协议有限（http）
- lua脚本的变更和nginx配置的修改需要重新启动，无法热更新
- 无可视化配置页面
```
- 可以作为流量网关，nginx层流量代理，负载均衡到Gateway做业务层的转发处理

#### nginx 怎么找
1. ps -ef | grep nginx (ps:显示系统进程)
2. whereis nginx 软件安装路径(whereis -- locate programs;The whereis utility checks the standard binary directories for the specified programs, printing out the paths of any it finds.The path searched is the string returned by the sysctl(8) utility for the ``user.cs_path'' string)
3. which nginx 运行文件所在路径(which -- locate a program file in the user's path;The which utility takes a list of command names and searches the path for each executable file that would be run had these commands actually been invoked.)
4. cd / && find - name 'nginx.conf'
nginx.conf => 基本的
vhost => 应用的

#### nginx 403
```
chmod -R 777
ps aux | grep "nginx: worker process" | awk '{print $1}'
```
<pre>
nginx 
root
</pre>

`vim nginx.conf`把 user  改成 root,即可;

#### firekylin nginx
```
ln -s /root/firekylin/nginx.conf /etc/nginx/conf.d/firekylin.conf
```
nginx.conf里面：
```
ln -s是一个Linux/Unix命令，用于创建软链接（Symbolic Link或称为Symlink）。软链接是一种类似于Windows系统中快捷方式的文件，它指向另一个文件或目录。其中，源文件或目录可以是绝对路径或相对路径，也可以是一个完整的URL。软链接可以跨越不同的文件系统，而硬链接只能在同一文件系统中使用。

软链接的用途：

- 简化文件路径名称
- 提高文件管理的灵活性与安全性
- 简化开发与维护工作

软链接的语法为：

```
ln -s source_file link_file
```

其中，source_file是源文件或目录的路径，link_file是链接文件的路径。执行此命令后，link_file将指向source_file，并且可以作为source_file的别名在系统中使用。
```

<pre>
~   #波浪线表示执行一个正则匹配，区分大小写

# location ~ /static/ {
# etag  on;
# expires  max;
# } 
</pre>

把     
<pre>
# etag  on;
# expires  max;
</pre>

都注释了，还是403

把`location ~ /static/ {}`
也注释了，就生效了

文档指路：http://nginx.org/en/docs/beginners_guide.html


#### kill nginx 服务
nohup = No HangUP
```
ps -ef|grep nginx
cd /usr/local/nginx/sbin
ls
./nginx -t
./nginx -s reload

kill -QUIT 28761
nohup /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf 
tail -2000f nohup.out
ps -ef|grep nginx
# 日志
# reload无效的时候
```

#### 前端history路由模式
```
location / {
  try_files $uri $uri/ /index.html;
}
```



#### 正则匹配

#### http server优先级

线上出过一个问题，之前一直没生效的CXP的配置生效了；原因是server优先级高于http,修改了server里面的一些跨域的配置；

## 应用场景
### 本地起nginx代理解决资源跨域或者连本地服务调试（嵌入移动端的页面）问题
```
nginx -v # 查看本机是否安装nginx, 如果没有安装homebrew安装下；
brew info nginx # 可获得nginx文件的配置位置
cd /usr/local/etc/nginx
code nginx.conf # 打开nginx配置文件
# 增加nginx server 80 下面的配置，这样test.company.cn就会访问到本地我们起的http://127.0.0.1:8886服务上 
http {
    include       mime.types;
    default_type  application/octet-stream;

   log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
    server_names_hash_bucket_size 128;
    client_header_buffer_size 32k;
    large_client_header_buffers 4 32k;
    client_body_buffer_size    8m;
    server_tokens off;
    ignore_invalid_headers   on;
    recursive_error_pages    on;
    server_name_in_redirect off;
    sendfile        on;
    tcp_nopush     on;
    tcp_nodelay    on;
    #keepalive_timeout  0;
    keepalive_timeout  65;
    server {
        listen 80;
        server_name test.company.cn;

        location / {
            proxy_pass http://127.0.0.1:8886;
        }
    }
}
# 修改系统hosts:
127.0.0.1 test.company.cn
127.0.0.1 localhost

# 这样，在浏览器里面输入test.company.cn就可以访问我们本地起的服务 http://127.0.0.1:8886 了；
```

### tengine
- http://tengine.taobao.org/
旧项目，接口server
Server: Tengine/2.2.3

新项目：接口server
Server: openresty/1.15.8.3

### 301
```
curl -i 'https://xxxx/qqq/thursday/xxxx'
HTTP/1.1 200 Connection established

HTTP/1.1 301 Moved Permanently
Server: nginx
Date: Thu, 21 Apr 2022 08:55:36 GMT
Content-Type: text/html
Content-Length: 169
Connection: keep-alive
Location: http://xxxx/qqq/thursday/xxxx/
Access-Control-Allow-Origin: *
Access-Control-Allow-Credentials: true
Access-Control-Allow-Methods: GET, POST, OPTIONS
Access-Control-Allow-Headers: DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type
Cache-Control: no-cache

<html>
<head><title>301 Moved Permanently</title></head>
<body>
<center><h1>301 Moved Permanently</h1></center>
<hr><center>nginx/1.18.0</center>
</body>
</html>

```
- 因为测试环境，前端多个项目配置了一个规则，规则这么配置的
```
location ~* ^/(qqq|xxx|xxxe|)/(env1|env2|env3|env4)/?(\w*) {
                root /neworiental/latest/;
                add_header 'Access-Control-Allow-Origin' '*';
                add_header 'Access-Control-Allow-Credentials' 'true';
                add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
                add_header 'Access-Control-Allow-Headers' 'DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type';
                add_header 'Cache-Control' 'no-cache';
                index index.html; 
                try_files $uri $uri/ /$1/$2/$3/index.html;
        }
```
- 这个时候，如果https://xxxx/qqq/thursday/xxxx 后面不加“/”，不是 https://xxxx/qqq/thursday/xxxx/ 的话，则会被重定向，因为nginx匹配规则有问题


## 配置实践
- 入口 html 文件设置 no-cache，其他资源文件设置 max-age 的缓存方式
- best-practice

#### 参考阅读
- https://mp.weixin.qq.com/s/0P8_lnVf2_zMzIBJ20qajA

### 问题
gpt流式
由于nginx默认开启了对请求内容的缓存，会导致即使使用了流式请求的方式，依然会在一段时间后一次性获取全部请求结果，所以需要修改链路上的相关配置。

chunked_transfer_encoding off; //禁用缓存
       proxy_buffering off; //禁用缓存
       proxy_cache off; //禁用缓存