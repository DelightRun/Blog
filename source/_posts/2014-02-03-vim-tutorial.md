----
layout: post
title: Vim基本操作总结
date: 2014-02-03 10:00:23 +0800
comments: true
categories: [Linux,Vim]
----

说起来VIM确实好用，不仅高效率，而且更重要的是 —— 能装逼。但是代价便是入门门槛较高。
所以在此我总结下自己常用的VIM命令，同时也是给我同学的一个入门教程。
VIM还有个官方自带教程，在命令行下输入

    $ vimtutor

<!-- more -->

## VIM的模式

* `x`删除当前字符
VIM的强大之处便在于它有很多种模式，传统的编辑器如记事本只是对应了VIM中的**编辑模式(Insert Mode)**。
细说起来VIM其实有很多种模式，但是实际上对我们来讲最常用也是最重要的是其中三种

* 一般模式(Normal Mode)
* 编辑模式(Insert Mode)
* 命令模式(Command Mode)

## 基本操作


以下介绍的所有命令都是**大小写敏感**的，而且是在**一般模式**和**命令模式**下执行，务必注意!!!

### 移动

#### 以字符为单位的移动

* `x`删除当前字符
* `k`上
* `j`下
* `h`左
* `l`右

#### 以词为单位的移动

* `x`删除当前字符
* `w`ord，下一个词
* `W`ord，下一个词，但是跳过标点
* `b`ackward，上一个词
* `B`你猜
* `e`nd，当前词的尾部

#### 行移动

* `x`删除当前字符
* `0`移动到0号字符，即行开头
* `^`跳到当前行第一个非空字符，意义同正则表达式
* `$`跳到行尾，意义同正则表达式

#### 段落移动

* `x`删除当前字符
* `{`上一段(以空白行分隔)
* `}`下一段(以空白行分隔)
* `%`跳到与当前括号对应的括号上

#### 跳跃移动

* `x`删除当前字符
* `/word`搜索输入的word，然后用`n`到下一个位置，用`N`到上一个位置
* `#`向前搜索当前所在字符
* `*`向后搜索当前所在字符
* `gd`跳到光标所在词的定义位置g(o)d(efine)
* `gg`跳到文件开头
* `G`跳到文件末尾
* `:x`跳到x
* `Ctrl+d`向下翻页
* `Ctrl+u`向上翻页

### 编辑

#### 插入

* `x`删除当前字符
* `i`nsert，在当前位置向前插入
* `I`在本行第一个字符前插入
* `a`fter，在光标当前位置向后插入
* `A`在本行末尾插入
* `o`向下插入一新行
* `O`你猜

#### 删除

* `x`删除当前字符
* `dd`删除当前行
* `dw`删除当前词
* `u`撤销操作

#### 复制粘贴

* `x`删除当前字符
* `yy`复制当前行
* `yw`复制当前词
* `p`粘贴
* `P`粘贴在当前位置之前

#### 保存

* `x`删除当前字符
* `:q`退出
* `:w`保存
* `:wq`保存并退出

## 进阶操作

这本来只是一个操作总结，为了ZM才写的多一点的，再多就成了教程了，那就说多了，所以以下仅仅是抛砖引玉。

### VIM操作原子化

VIM操作都是原子化的，所以可以组合，比如`16j`就是向下移动16行，`3dw`就是删除3个词，无数情况，详见vimtutor。

### 高效编辑

* `di"`光标在""之间，则删除""之间的内容
* `yi(`你猜
* `vi[`选中[]之间的内容

以上三种、请举一反三，组合很多

* `dtx`从光标位置开始删除字符，直到遇到第一个字符`x`
* `ytx`你猜

## 更多

VIM绝对是博大精深，还有标记啊、宏啊、一堆插件啊、配置啊什么的，慢慢研究吧。用好了绝对超神，还能装逼。
据说微软许多大牛放着VS不用，用VIM、Emacs写C#。

##### 参考资料:

* [Git时代的VIM不完全使用教程][1]，一篇博文，本文就是照着那个写的，而且那个博客也不错
* [超强VIM配置][2]，我在Github里fork的一个超强的配置好的VIM，插件和配置文件都弄好了，很酷

[1]: http://beiyuu.com/git-vim-tutorial/
[2]: https://github.com/DelightRun/vim
