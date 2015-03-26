---
layout: post
title: "使用Git部署网站"
date: 2015-03-26 12:00:30 +0800
comments: true
categories: Git, Linxu
---

以前部署网站经常使用FTP或scp方式，但这两种方式不仅操作麻烦而且有无法进行版本控制、用户权限等诸多问题。
使用Git我们能方便的部署网站，何乐而不为呢。

<!-- more -->

一、安装Git与SSH
================

    $ sudo yum install git git-core ssh

二、建立git用户
==============

1. 新建git用户并设置密码
  
    $ sudo useradd git
    $ passwd git

2. 禁止git用户通过shell登录

    $ sudo vim /etc/passwd

将*git:x:1001:1001:,,,:/home/git:/bin/bash*
修改为*git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell*

三、建立Git裸仓库
================

    $ cd /path/to/your/git/repo
    $ sudo git init --bare your_repo_name.git
    
并修改权限

    $ sudo chown -R git:git your_repo_name.git

四、设置Git hook以实现自动部署
=============================

    $ cd your_repo_name.git/hooks
    $ sudo vim post-receive

写入以下内容

    #!/bin/sh
    GIT_WORK_TREE=/path/to/your/website git checkout -f

最后加上执行权限

    $ chmod +x post-receive

**注意：/path/to/your/website目录需自己手动创建**
