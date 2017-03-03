---
title: linux 计划任务
date: 2016/10/13 00:31:30
category: linux
---

### crond

    crond linux 用来周期性执行某些任务或处理某些事情的一个守护进程，crond 进程会每分钟检查
    是否有要执行的任务并自动执行


<!-- more -->

### 系统任务调度

``` bash

# /etc/crontab 系统任务调度的配置文件
SHELL=/bin/bash  # 指定系统使用那个 shell
PATH=/sbin:/bin:/usr/sbin:/usr/bin  # 指定系统命令执行命令的路径
MAILTO=root # 将通过电子邮件发送任务信息给用户，值为空则不发送
HOME=/ # 执行命令或脚本的主目录    

```

### 用户任务调度

    用户定期要执行的任务，可以使用 crontab 工具定制，配置文件保存在 /var/spool/cron/{用户名}

    权限控制
    /etc/cron.deny  # 该文件中所列用户不允许使用 crontab 命令
    /etc/cron.allow # 该文件中所列用户允许使用 crontab 命令

### crontab tool

    crontab [-u user] file
    crontab [-u user] [-e | -l | -r]

    -u   ：指定某个用户的 crontab
    file ：使用 file 载入任务
    -e   ：编辑 crontab
    -l   ：显示 crontab
    -r   ：删除 /var/spool/cron 某个用户的 crontab 文件，默认当前用户

### crontab 文件说明

    minute hour day  month week command
    0-59   0-23 1-31 1-12  0-7

    * ：所有可能
    , ：指定列表
    - ：指定区间
    / ：指定间隔频率

    run-parts ：指定执行该目录下的脚本
