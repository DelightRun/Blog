---
layout: post
title: Ubuntu下安装Ruby 2.1.2和Rails
date: 2014-08-29 10:00:23 +0800
comments: true
categories: [Web,Ruby on Rails]
---

在Ubuntu13.04下使用`apt-get`安装的Ruby版本为`1.9.3`，
本文将介绍如何在Ubuntu下安装最新的`Ruby 2.1.2`

<!-- more -->

###安装rbenv

**首先**，手动安装rbenv

    $ git clone git://github.com/sstephenson/rbenv.git ~/.rbenv
    # 用来编译安装 ruby
    $ git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
    # 通过 gem 命令安装完 gem 后无需手动输入 rbenv rehash 命令, 推荐
    $ git clone git://github.com/sstephenson/rbenv-gem-rehash.git ~/.rbenv/plugins/rbenv-gem-rehash
    # 通过 rbenv update 命令来更新 rbenv 以及所有插件, 推荐
    $ git clone https://github.com/rkh/rbenv-update.git ~/.rbenv/plugins/rbenv-update

**然后**，在`~/.bashrc`里添加如下内容

    export PATH="$HOME/.rbenv/bin:$PATH"
    eval "$(rbenv init -)"

**最后**，执行以使`~/.bashrc`生效

    $ source ~/.bashrc

*注意*：其他Linux发行版如CentOS中为`~/.bash_profile`

###安装Ruby

由于在国内*你懂的*的网络环境下，直接使用rbenv下载安装Ruby速度非常慢，
所以我们使用如下技巧加快安装速度

**首先**，从淘宝的Ruby镜像处下载安装包

    $ wget http://ruby.taobao.org/mirrors/ruby/2.1/ruby-2.1.2.tar.gz -O ~/.rbenv/versions/ruby-2.1.2.tar.gz

**然后**，配置环境变量

    $ env RUBY_BUILD_MIRROR_URL=file://$HOME/.rbenv/versions/ruby-2.1.2.tar.gz#~/.rbenv/bin/rbenv install 2.1.2

*注意*：文件地址后面的`#`及其以后内容不能省略

**最后**，安装Ruby 2.1.2

    $ rbenv install 2.1.2

###替换Gems源

还是由于*你懂的*的原因，在国内直接使用`gem install`命令是不行的，
所以我们要将其源替换为淘宝的Gems源

    $ gem sources -r https://rubygems.org/
    $ gem sources -a https://ruby.taobao.org/
    $ gem sources -l

执行完成后会看到

    *** CURRENT SOURCES ***

    https://ruby.taobao.org

###安装Rails

接下来直接安装`rails`即可

    $ gem install rails
