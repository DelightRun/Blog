---
layout: post
title: Ubuntu下搭建LAMP服务器
date: 2014-09-24 20:06:22 +0800
comments: true
categories: [Linux,服务器]
---

本文讲述如何在Ubuntu下搭建LAMP服务器的大体流程

> LAMP: Linux + Apache + MySQL + PHP

<!-- more -->

##安装Apache2

搭建LAMP服务器第一步是安装Apache2，在Ubuntu下简单到只需如下一行命令：

    $ sudo apt-get install apache2

##安装PHP

安装PHP需要安装两个包，一是`PHP5`本身，二是Apache2的`PHP模块`，安装命令如下：

    $ sudo apt-get install php5 libapache2-mod-php5

##安装MySQL

安装MySQL需要安装服务端程序`mysql-server`、PHP的MySQL扩展`php5-mysql`，
同时一般还会安装MySQL的命令行客户端`mysql-client`：

    $ sudo apt-get install mysql-server mysql-client php5-mysql

**注意：**安装过程中的`root`账户密码你可以随便填，反正第一次用这个密码你一定无法登陆，
下面我们将叙述如何解决该问题

##配置MySQL的root密码

如果你在用上述命令安装完MySQL后使用命令：

    $ mysql -uroot -p你的密码

一定会出现`error 1045`的错误，具体原因我也没完全搞清，有谁知道请[不吝赐教](mailto:changxu.mail@gmail.com)

解决方案是，首先查看文件`/etc/mysql/debian.cnf`文件：

    $ sudo cat /etc/mysql/debian.cnf

**注意**：此处的`sudo`必不可少

然后会看到下面这样的内容：

    # Automatically generated for Debian scripts. DO NOT TOUCH!
    [client]
    host     = localhost
    user     = debian-sys-maint
    password = 一个乱七八糟的字符串
    socket   = /var/run/mysqld/mysqld.sock
    [mysql_upgrade]
    host     = localhost
    user     = debian-sys-maint
    password = 同上面那个乱七八糟的字符串
    socket   = /var/run/mysqld/mysqld.sock
    basedir  = /usr

注意到其中的`user`和`password`两行，那边是安装过程中系统提供的默认账户密码，于是我们这样登陆：

    $ mysql -udebian-sys-maint -p那个乱七八糟的字符串

这时候我们就能进入MySQL的命令行管理后台，我们在此设置`root`的密码：

    > USE mysql;
    > UPDATE user SET password=PASSWORD('你要设置的密码') WHERE user='root';
    > flush privilege;
    > exit;

这时候我们就能用`root`账户登陆MySQL

    $ mysql -uroot -p你的root密码

##启动Apache2

现在我们启动`apache2`服务：

    $ sudo service apache2 start

然后我们访问[http://localhost/](http://localhost/)，应该能看到一个网页写着：

    It Works!

至此，一台基于Ubuntu、功能正常、有数据库、支持PHP语言的服务器就搭建完成了，下面是附加部分

##可选：安装PHPMyAdmin

PHPMyAdmin是一款基于PHP的数据库管理网站，在Ubuntu下安装非常简单：

    $ sudo apt-get install phpmyadmin

然后我们将PHPMyAdmin的配置复制至apache2的配置文件夹下：

    $ sudo cp /etc/phpmyadmin/apache.conf /etc/apache2/sites-available/phpmyadmin.conf
    $ sudo ln -s /etc/apache2/sites-available/phpmyadmin.conf /etc/apache2/sites-enabled/phpmyadmin.conf

最后重启apache2：

    $ sudo service apache2 restart

然后访问[http://localhost/phpmyadmin/](http://localhost/phpmyadmin/)，用你的数据库账号密码登陆

###Enjoy!
