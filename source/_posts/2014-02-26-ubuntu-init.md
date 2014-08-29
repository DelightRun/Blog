---
layout: post
title: 我的Ubuntu配置
date: 2014-02-26 20:30:30 +0800
comments: true
categories: [Linux]
---

##配置root密码

    $ sudo passwd root

##更换软件源

备份软件源配置

    $ sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

打开配置文件

    $ sudo gedit /etc/apt/sources.list

更改配置文件为如下内容

##安装输入法

####卸载ibus
    
    $ sudo apt-get remove ibus
    $ sudo apt-get remove ibus-googlepinyin

####安装fcitx和搜狗拼音

    $ sudo add-apt-repository ppa:fcitx-team/nightly && sudo apt-get updates
    $ sudo apt-get install fcitx-sogoupinyin

##安装chrome

去[chrome网站](https://www.google.com/intl/zh-CN/chrome/)上下

##terminator

####安装terminator

    $ sudo apt-get install terminator

####安装Solarized主题

1.安装主题

    $ mkdir -p ~/.config/terminator/config
    $ curl https://raw.github.com/ghuntley/terminator-solarized/master/config > ~/.config/terminator/config

2.配置dircolors

    $ curl https://raw.github.com/seebi/dircolors-solarized/master/dircolors.ansi-dark > ~/.dircolors

##安装curl
    
    $ sudo apt-get install curl

##安装vim

详见[我的vim](https://github.com/DelightRun/VimConfiguration)

##剩下的想起来再补充
