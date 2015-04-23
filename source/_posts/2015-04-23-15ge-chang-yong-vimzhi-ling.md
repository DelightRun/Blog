---
layout: post
title: "15个常用Vim指令"
date: 2015-04-23 14:52:58 +0800
comments: true
categories: Linux, Vim
---

> 列举15个不常见但很有用的Vim指令，[原帖](http://saebbs.com/forum.php?mod=viewthread&tid=34284&extra=page%3D8)

<!--more-->

+ `:x`相当于`:wq`
+ `Ctrl+R`后输入`=`可当计算器用
+ 查找连续重复单词的正则表达式——`\(\<\w\+\>)\)\_s*\1
+ 设置缩写`:ab [缩写] [全部]`
+ `:w !sudo tee %`直接以root保存
+ `ggVGg?`将屏幕内容以ROT13编码以让别人看不懂
+ 插入模式下按`Ctrl+n`自动补全
+ `:diffthis` + `:vsp [文件2]` + `:diffoff`组合指令分离进行文件对比
+ `:earlier 1m`回退到一分钟以前的状态，`:later`则是相反转换
+ 将光标放在(或[或{或"上，使用`di对应符号`可以删除()或{}或[]或""内的内容，如`di[`
+ `dt[标记]`会删除从光标到标记之间的内容（标记不删）
+ `%!xxd`将Vim变成十六进制编辑器，恢复则用`%!xxd -r`
+ `zz`将光标下的文字置于屏幕中央
+ `Ctrl+o`跳到光标上一个位置，`Ctrl+i`则相反
+ `%TOhtml`将文档转换成HTML

> 更多Vim技巧请参考[Vim Tips Wiki](http://vim.wikia.com/wiki/Vim_Tips_Wiki)