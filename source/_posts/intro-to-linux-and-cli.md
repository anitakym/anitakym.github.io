---
title: intro-to-linux-and-cli
date: 2021-04-21 15:30:50
tags:
---
https://btholt.github.io/complete-intro-to-linux-and-the-cli/

notes from 《complete-intro-to-linux-and-the-cli》

## 文档精读：


### Cron
Linux有cron的功能，可以定时跑任务

#### cron folders
放在以下任何一个文件夹中的任何脚本都将按时间表运行

/etc/cron.daily
/etc/cron.hourly
/etc/cron.monthly
/etc/cron.weekly

确保有权限就行，可以通过```sudo chmod +x <file>```
这里面的内容以root身份运行
#### crontab
如果你需要一个更明确的时间表（比如每五分钟，每隔一个星期四，每六个月，等等），那么可以使用crontab。用crontab可以定义一个cron时间表来执行脚本。
```
mkdir -p ~/temp-files # 在home目录下
cd ~/temp-files
touch file-$(date +%s).txt 
```
$(date +%s)，从1970到现在，过去了多少秒

- crontab - maintains crontab files for individual users
<pre>
-e     Edits the current crontab using the editor specified by the VISUAL or EDITOR environment variables.   After  you
              exit from the editor, the modified crontab will be installed automatically.
</pre>
```
crontab -e
crontab -e ubuntu -e
```

https://crontab.guru/
规则记起来也不是很好记，可以借助上面的网站进行参考

定时任务的处理记得保证逻辑完备