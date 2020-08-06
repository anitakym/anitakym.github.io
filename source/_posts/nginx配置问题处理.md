---
title: nginx配置问题处理
date: 2020-08-03 16:46:32
tags:
    - nginx
---

#### nginx 403
chmod -R 777


ps aux | grep "nginx: worker process" | awk '{print $1}'

nginx 
root

vim nginx.conf
把 user  改成 root;

即可


#### firekylin nginx
ln -s /root/firekylin/nginx.conf /etc/nginx/conf.d/firekylin.conf

nginx.conf里面：
```
    #location ~ /static/ {
     #   etag         on;
       #  expires      max;
    #} 
```

这行注释掉，报取static里面文件的403错误就好了

~      #波浪线表示执行一个正则匹配，区分大小写

把     #   etag         on;
       #  expires      max;

都注释了，还是403

把location ~ /static/ {}
也注释了，就生效了


http://nginx.org/en/docs/beginners_guide.html