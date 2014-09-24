---
layout: post
title: 我的Ubuntu配置
date: 2014-02-26 20:30:30 +0800
comments: true
categories: [Linux]
---

> 本文为我在安装Ubuntu时使用的配置。

<!-- more -->

##配置root密码

    $ sudo passwd root

##更换软件源

*Step 1.* 备份软件源配置

    $ sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

*Step 2.* 打开配置文件

    $ sudo gedit /etc/apt/sources.list

*Step 3.* 更改配置文件为如下内容并保存（在此使用阿里软件源）

	deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
	deb http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
	deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
	deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
	deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse
	deb-src http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
	deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
	deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
	deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
	deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse

*Step 4.* 刷新软件源
    
    $ sudo apt-get update

##安装输入法

####卸载ibus
    
    $ sudo apt-get remove ibus
    $ sudo apt-get remove ibus-googlepinyin

####安装fcitx和搜狗拼音

    $ sudo add-apt-repository ppa:fcitx-team/nightly && sudo apt-get updates
    $ sudo apt-get install fcitx-sogoupinyin

##安装Chrome并配置翻墙

*Step 1.* 去[Chrome官网](https://www.google.com/intl/zh-CN/chrome/)上下载并安装Chrome浏览器

*Step 2.* 使用Shadowsocks进行翻墙，[客户端列表](https://github.com/clowwindy/shadowsocks/wiki/Ports-and-Clients)

*Step 3.* 给Chrome安装自动代理切换插件[SwitchySharp](/attachments/SwitchySharp.crx)，并导入[备份的配置](/attachments/SwitchyOptions.bak)

##terminator

####安装terminator

    $ sudo apt-get install terminator

####安装色彩主题

1.安装主题

    $ mkdir -p ~/.config/terminator/config
    $ curl https://raw.github.com/ghuntley/terminator-solarized/master/config > ~/.config/terminator/config

2.配置dircolors

    $ sudo apt-get install curl
    $ curl https://raw.github.com/seebi/dircolors-solarized/master/dircolors.ansi-dark > ~/.dircolors

##安装vim

可参考[我的Vim配置](https://github.com/DelightRun/VimConfiguration)

##开发环境配置

*TODO: 待续*
