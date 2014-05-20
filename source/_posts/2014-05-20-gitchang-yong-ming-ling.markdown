--- 
layout: post
title: "Git常用命令"
date: 2014-05-20 22:50:43 +0800
comments: true
published: false
categories: 
---

##术语中英文对照表
`仓库` <=> `repository`
`暂存区` <=> `stage`

##关于提交的某些代号
+ `HEAD`代表版本库最近一次提交
+ `^`代表父提交，如：
    * HEAD^代表上一次提交
    * HEAD^^代表上上一次提交
+ `^<N>`代表第N个父提交，如果某个提交有多个父提交
+ `~<N>`代表第N个祖先提交，如：`HEAD~5`相当于`HEAD^^^^^`

###配置用户名和邮件
    $ git config --global user.name "name"
    $ git config --global user.email "email"

###配置命令别名
全局配置：
    $ sudo git config --system alias.st status
    $ sudo git config --system alias.ci commit
    $ sudo git config --system alias.co checkout
    $ sudo git config --system alias.br branch
单个用户配置:
    $ git config --global alias.st status
    $ git config --global alias.ci commit
    $ git config --global alias.co checkout
    $ git config --global alias.br branch

###建立仓库
    $ git init              # 在本目录下初始化
    $ git init <directory>  # 新建<directory>目录并在其中初始化
*可添加`--bare`参数，以新建不含工作区的裸仓库*

###查看工作区状态
    $ git status
    $ git status -s     # 精简显示

###比较
    $ git diff              # 比较工作区与暂存区
    $ git diff HEAD         # 比较工作区与版本库
    $ git diff --cached     # 比较暂存区与版本库

###添加文件到暂存区
    $ git add <file>    # 暂存单个文件
    $ git add .         # 暂存所有改动的文件
    $ git add -A
*在git中经常用`.`表示所有符合条件的文件，下同*

###提交
    # 提交
    $ git commit
    $ git commit -m '提交说明'
    
    # 暂存所有改动并提交（不推荐）
    $ git commit -a
    $ git commit -a -m '提交说明'
    
    # 更改上次提交的说明
    $ git commit -amend

###查看提交日志
    $ git log
    $ git log --raw
    $ git log --oneline

    #显示跟踪链
    $ git log --graph
    $ git log --raw --graph
    $ git log --oneline --graph
*可通过添加`-{num}`参数来限定显示的条目数，如-1,-2,-13*
    
###撤销修改
    # 撤销至暂存区的内容
    $ git checkout -- <file>
    $ git checkout -- .
    
    # 撤销至版本库的内容
    $ git checkout HEAD <file>
    $ git checkout HEAD .

###状态的保存与恢复
    $ git stash         # 保存
    $ git stash pop     # 恢复
