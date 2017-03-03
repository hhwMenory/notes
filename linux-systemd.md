---
title: linux systemd
date: 2017/03/02 09:42:18
category: linux
---

### 基本概念

``` bash 
    
    # 单元 unit
    
        ## service 
        ## socket
        ## device
        ## mount
        ## automount
        ## swap
        ## target
        ## timer
        ## snapshot

```

<!-- more -->

### unit 文件的编写

``` bash

    配置单元文件以 .service 为后缀，文件分为三小节：
    
        [Unit]
        Description=xxx                         # 描述信息
        [Service]
        EnvironmentFile=/etc/sysconfig/sshd 
        ExecStartPre=/usr/sbin/sshd-keygen      # 定义启动服务之前应该运行的命令
        ExecStart=/usrsbin/sshd –D $OPTIONS     # 定义启动服务的具体命令行语法
        ExecReload=/bin/kill –HUP $MAINPID
        KillMode=process
        Restart=on-failure
        RestartSec=42s
        [Install]
        WantedBy=multi-user.target              # 表明这个服务是在多用户模式下所需要的

        [Unit].Requires=vvv                     # 定义表明某服务启动的时候 vvv 也必须被启动
        [Install].Alias=xxx                     # 定义本单元的别名
        
        # /etc/systemd/system/*.want/ 目录相当于[Unit].wants 即*单元启动时，还要启动该目录
          下配置单元文件的单元
          
        [Mount]
        What=debugfs
        Where=/sys/kernel/debug
        Type=debugfs
        
        ===> mount  –t debugfs      /sys/kernel/debug  debugfs
                    指定文件系统的类型  要挂载的设备         设备在系统的挂载点
                  
```

### Systemd 命令

``` bash

    systemctl start xxx.service
    systemctl stop xxx.service
    systemctl restart xxx.service
    systemctl reload xxx.service
    systemctl status xxx.service
    systemctl enable xxx.service
    systemctl disable xxx.service
    systemctl is-enabled xxx.service
    systemctl list-unit-files --type=service
    systemctl daemon-reload
    systemctl isolate multi-user.target

    systemctl reboot        # 重启机器
    systemctl poweroff      # 关机
    systemctl suspend       # 待机
    systemctl hibernate     # 休眠
    systemctl hybrid-sleep  # 混合休眠模式（同时休眠到硬盘并待机）

```

