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

五、在本地添加远程仓库
==================

	$ git remote add origin ssh://git@your_server:/path/to/your/repo.git

接下来就可以正常的*git push origin*了

Extra、使用公钥进行SSH认证
=======================

每次登陆SSH都需要输入密码是一件非常麻烦的事情，所以我们使用公钥认证。

首先，在本地生成公钥——输入以下命令并按提示操作

	$ ssh-keygen -t rsa -C "your_email@youremail.com"
	
然后，打开*~/.ssh*目录下的*id_rsa.pub*文件，复制里面的内容，

最后，将刚才复制的内容粘贴至服务器上的*/home/git/.ssh/authorized_keys*文件里（没有则新建）