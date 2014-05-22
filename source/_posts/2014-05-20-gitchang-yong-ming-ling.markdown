--- 
layout: post
title: "Git常用命令"
date: 2014-05-20 22:50:43 +0800
comments: true
categories: 
---

##术语中英文对照表
+ `仓库`      <=>     `repository`
+ `工作区`    <=>     `working directory`
+ `暂存区`    <=>     `staging area`

##关于提交的某些代号
+ `HEAD`代表版本库最近一次提交
+ `^`代表父提交，如：
    * HEAD^代表上一次提交
    * HEAD^^代表上上一次提交
+ `^<N>`代表第N个父提交，如果某个提交有多个父提交
+ `~<N>`代表第N个祖先提交，如：`HEAD~5`相当于`HEAD^^^^^`
+ `@{N}`代表N次修改前的值，如：`HEAD@{1}`代表HEAD上次被修改前的值
+ 每个分支的名称也指向某个独一无二的提交，所以下面的<commit>也可以是其他分支名

###配置用户名和邮件
    $ git config --global user.name "name"
    $ git config --global user.email "email"

###配置命令别名
    #全局配置：
    $ sudo git config --system alias.st status
    $ sudo git config --system alias.ci commit
    $ sudo git config --system alias.co checkout
    $ sudo git config --system alias.br branch

    #单个用户配置:
    $ git config --global alias.st status
    $ git config --global alias.ci commit
    $ git config --global alias.co checkout
    $ git config --global alias.br branch

###建立仓库
    # 新建
    $ git init [--bare]                  # 在本目录下初始化
    $ git init [--bare] <directory>      # 新建<directory>目录并在其中初始化

    # 克隆
    $ git clone <repository>
    $ git clone <repository> <directory>
    $ git clone --bare <repository>         # 克隆下来不包含工作区的裸版本
    $ git clone --mirror <repository>       # 克隆工作区，不过可以用git fetch和上游版本库持续同步

###远程仓库操作
    # 添加远程仓库
    $ git remote add <remote> <url>

    # 查看远程仓库列表
    $ git remote -v

    # 更改远程仓库URL
    $ git remote set-url <remote> <url>

    # 单独设置push和fetch的地址
    $ git remote set-url --push <remote> <url>      # 设置push操作的地址
    $ git remote set-url --fetch <remote> <url>     # 设置fetch操作的地址

    # 从全部远程仓库获得更新
    $ git remote update
    
    # 删除远程仓库
    $ git remote rm <remote>

###比较
    # 比较工作区与暂存区
    $ git diff              # 比较全部改动，下同
    $ git diff -- <path>    # 比较特定文件，下同

    # 比较工作区与某次提交
    $ git diff <commit>
    $ git diff <commit> -- <path>

    # 比较暂存区与HEAD
    $ git diff --cached
    $ git diff --cached -- <path>

    # 比较暂存区与某此提交
    $ git diff --cached <commit>
    $ git diff --cached <commit> -- <path>

    # 比较两次提交
    $ git diff <commit1> <commit2>
    $ git diff <commit1> <commit2> -- <path>

    # 比较两个文件
    $ git diff <path1> <path2>

###删除及移动
    $ git rm <path1> <path2> <etc.>     # 删除
    $ git mv <path1> <path2> <etc.>     # 移动

###追溯文件修改记录
    $ git blame <path>
    $ git blame -L n,m <path>   # 限定查看范围，m可以是相对坐标，如：-L 6,+5为查看[6,10]行

###查看工作区状态
    $ git status
    $ git status -s             # 精简显示
    $ git status --ignore       # 查看被忽略的文件
    $ git status --ignore -s    # 同上，只不过精简显示

###添加文件到暂存区
    $ git add <path>    # 暂存单个文件
    $ git add .         # 暂存所有文件
    $ git add -A        # 暂存所有改动及新增的文件
    $ git add -u        # 暂存删除的文件和目录
    $ git add -i        # 交互式暂存, 自己试试、无害
*在git中经常用`.`表示所有符合条件的文件，下同*

###替换暂存区文件
    $ git reset                         # 用HEAD指向的提交重置整个暂存区
    $ git reset -- <path>               # 用HEAD指向提交替换暂存区指定文件
    $ git reset <commit> -- <path>      # 用<commit>替换暂存区指定文件，不重置HEAD值

###重置HEAD
    # 更改HEAD与HEAD所指分支（如一般为master）指向的提交
    $ git reset --soft <commit>

    # 更改HEAD与HEAD所指分支（如一般为master）指向的提交，并替换暂存区
    $ git reset [--mixed] <commit>      # --mixed是默认参数，没有也行

    # 更改HEAD与HEAD所指分支（如一般为master）指向的提交，并替换暂存区与工作区
    $ git reset --hard <commit>

###提交
    # 提交
    $ git commit
    $ git commit -m '提交说明'
    
    # 暂存所有改动并提交（不推荐）
    $ git commit -a
    $ git commit -a -m '提交说明'
    
    # 更改上次提交的说明
    $ git commit -amend

    # 重用某此提交的说明
    $ git commit -C <commit>

###推送至远程仓库
    $ git push <remote> <branch>    # 推送至远程仓库指定分支

###从远程仓库拉取
    # 仅拉取不合并
    $ git fetch             # 默认获取origin
    $ git fetch <remote>    # 从指定仓库获取

    # 拉取并合并，相当于git fetch + git merge
    $ git pull              # 默认拉取并合并origin
    $ git pull <remote>     # 从指定仓库拉取并合并

###提交一次反转提交
>注：书上使用“反转提交”，但我认为这样有歧义，我管它叫“提交一次反转提交”
    
    # 反向提交
    $ git revert <commit>
    $ git revert <commit1>..<commit2>

    # 只改变工作区与暂存区而不产生新提交
    $ git revert <commit>
    $ git revert <commit1>..<commit2>

    # 遇到冲突
    $ git revert --continue     # 解决冲突后暂存更改，然后恢复反转提交
    $ git revert --quit         # 忽略这次失败的翻转，继续执行
    $ git revert --abort        # 终止反转提交，回到之前提交

###查看某次提交详情
    $ git show              # 显示HEAD提交详情
    $ git show <commit>     # 显示<commit>提交详情

###查看提交日志
    $ git log [-<num>] [--pretty=<pretty>] [-stat] [--graph]
*`-stat`参数自己试试吧*

*`<num>`为限定显示的数量，<num>可以是1,2,3等*

*`<pretty>`可以是`fuller`,`raw`,`oneline`,默认为`raw`*

###更改工作区文件
    # 用暂存区中的文件覆盖工作区中的文件
    $ git checkout -- <path>
    $ git checkout .
    
    # 维持HEAD不变，用<commit>所指向的提交同时覆盖暂存区和工作区文件
    $ git checkout <commit> -- <path>
    $ git checkout <commit> .

###切换HEAD位置
    $ git checkout <commit>

###汇总显示工作区、暂存区与HEAD的差异
    $ git checkout HEAD

###分支管理
    # 列出本地分支
    $ git branch

    # 创建分支
    $ git branch <branch>              # 从HEAD创建
    $ git branch <branch> <commit>     # 从提交<commit>开始创建

    # 删除分支
    $ git branch -d <branch>    # 检查要删除的分支是否已合并到其他分支，未合并则不删除
    $ git branch -D <branch>    # 强制删除，不管是否合并

    # 重命名分支
    $ git branch -m <oldbranch> <newbranch>

    # 远程仓库分支操作
    $ git push <remote> <local-branch>:<remote-branch>     # 添加
    $ git push <remote> :<remote-branch>                   # 删除

###合并分支
    $ git merge <branch>                # 将<branch>合并至当前分支并提交
    $ git merge --no-commit <branch>    # 仅合并不提交
*从远程仓库fetch下来的分支一般为`<remote>/<branch>`，如`origin/master`*

###变基操作
    # 将(<since>, <until>]之间的提交（不含<since>）嫁接到HEAD后
    $ git rebase <since>            # <until>为空，则默认为最后一次提交，下同
    $ git rebase <since> <until>

    # 将(<since>, <until>]之间的提交（不含<since>）嫁接到<newbase>后
    $ git rebase --onto <newbase> <since>
    $ git rebase --onto <newbase> <since> <until>

    # 交互式变基操作
    $ git rebase -i

    # 变基遇到冲突
    $ git rebase --continue     # 解决冲突后暂存更改，然后恢复变基操作
    $ git rebase --skip         # 跳过当前提交
    $ git rebase --abort        # 终止变基操作，回到之前提交

###进度的保存与恢复相关
    # 保存
    $ git stash
    $ git stash save '保存说明'
    
    # 查看保存的进度
    $ git stash list
    
    # 恢复
    $ git stash pop             # 从最近的保存恢复
    $ git stash pop <stash>     # 从<stash>恢复

    # 删除保存的状态
    $ git stash drop            # 删除最近保存记录
    $ git stash drop <stash>    # 删除<stash>
    $ git stash clean           # 全部删除

    # 基于进度创建分支
    $ git stash branch <branchname> <stash>

###删除本地多余的文件与目录
    $ git clean -nd     # 删除测试
    $ git clean -fd     # 强制删除

###打标签/里程碑
    # 显示当前版本库的标签列表
    $ git tag
    $ git tag -n<num>       # 限定显示<num>个
    $ git tag -l <match>     # 用通配符过滤

    # 为HEAD打标签
    $ git tag <tag>
    $ git tag -m '标签说明信息' <tag>

    # 为某次提交打标签
    $ git tag <tag> <commit>
    $ git tag -m '标签说明信息' <tag> <commit>

    # 删除标签
    $ git tag -d <tag>

    # 远程仓库标签操作
    $ git push <remote> <tag>       # 添加
    $ git push <remote> :<tag>      # 删除

###打包/归档
    $ git archive -o <归档文件名> <commit>
    $ git archive -o <归档文件名> <commit> <path1> <path2> <etc.>

###其他常用功能
    $ git bisect    # 这个功能很强大、但是有点复杂，所以就不想细说了
    $ git rc        # 清理版本库中的冗余、垃圾、过期信息
