---
layout: post
title: "搭建Shadowsocks服务器并开启FastOpen优化"
date: 2015-09-30 18:05:05 +0800
comments: true
categories: Linux, Shadowsocks
---

在Ubuntu系统上搭建Shadowsocks服务器并开启FastOpen优化，CentOS系统操作类似，只不过是使用`yum`代替`apt-get`

<!-- more -->

# 第一步：安装Shadowsocks

    $ sudo apt-get install m2crypto python-pip
    $ pip install shadowsocks
    
# 第二步：编写配置文件

新建文件`/etc/shadowsocks/config.json`，内容如下（`//`后面的为注释，实际文件中不需要）：

    {
        "server": "你的服务器公网IP地址",
        "server_port": 8388,    //或其他任何未被占用的端口号，最好自己选个不常用的
        "local_address": "127.0.0.1",
        "local_port": 1080,     // 保持不变
        "password": "自己设定的密码",
        "timeout": 600,
        "method": "aes-256-cfb",
        "fast_open": true       // 仅限Linux 3.5+内核并开启FastOpen功能，否则请设置为false
    }

# 第三步：开启操作系统的FastOpen

> 注意！FastOpen仅支持Linux 3.5+的内核，请使用`cat /proc/version`命令查看内核版本是否满足需求

编辑`/etc/security/limits.conf`文件，增加如下两行：

    * soft nofile 51200
    * hard nofile 51200

执行`ulimit`命令：

    $ sudo ulimit -n 51200
    
编辑`/etc/sysctl.conf`文件，添加如下内容：

    fs.file-max = 51200
   
    net.core.netdev_max_backlog = 250000
    net.core.somaxconn = 4096
    
    net.ipv4.tcp_syncookies = 1
    net.ipv4.tcp_tw_reuse = 1
    net.ipv4.tcp_tw_recycle = 0
    net.ipv4.tcp_fin_timeout = 30
    net.ipv4.tcp_keepalive_time = 1200
    net.ipv4.ip_local_port_range = 10000 65000
    net.ipv4.tcp_max_syn_backlog = 8192
    net.ipv4.tcp_max_tw_buckets = 5000
    net.ipv4.tcp_fastopen = 3
    net.ipv4.tcp_rmem = 4096 87380 67108864
    net.ipv4.tcp_wmem = 4096 65536 67108864
    net.ipv4.tcp_mtu_probing = 1
    net.ipv4.tcp_congestion_control = hybla
    
    # 注意：Digital Ocean请勿添加下面四行，因为配置文件中已存在
    net.core.rmem_max = 67108864
    net.core.wmem_max = 67108864
    net.ipv4.tcp_rmem = 4096 87380 67108864
    net.ipv4.tcp_wmem = 4096 65536 67108864

查看可用的拥塞控制算法：

    $ sysctl net.ipv4.tcp_available_congestion_control

如果有hybla算法，请开启：

    $ sudo /sbin/modprobe tcp_hybla
    
否则用cubic算法：

    $ sudo /sbin/modprobe tcp_cubic

最后使配置文件生效：

    $ sudo sysctl -p
    
# 第四步，启动Shdadowsocks

    $ ssserver -c /etc/shadowsocks/config.json
    
关于开机自启动配置、后台运行配置等，请参看其他Linux系统教程，推荐使用**Supervisor**进行配置。
    
