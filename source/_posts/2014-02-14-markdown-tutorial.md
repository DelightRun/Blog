---
layout: post
title: Markdown概述与标记总结
date: 2014-02-14 20:30:30 +0800
comments: true
categories: [Octopress,前端]
---

#概述

相较于HTML这种重量级文本标记语言，Markdown是一种轻量级的文档标记语言。

从Markdown可以非常容易的生成HTML。关于Markdown的更多介绍请自行Google。
    
> 请关注下[reStructuredText](http://docutils.sourceforge.net/rst.html)和[Sphinx](http://sphinx-doc.org/)，他们经常被用于生成Python的文档。

<!-- more -->

#语法标记

##段落和换行

一个或多个连续的文本行可作为一个Markdown的段落，它的前后要有一个或多个空行

> Markdown不会将单独一个换行符转为换行，若想在Markdown中插入一个换行的话，在插入处先按两个以上空格再回车。

##标题

+ 类Setext式:

    1. 一级标题`<h1>` -- `=`
    2. 二级标题`<h2>` -- `-`

+ 类Atx式:

    1. 一级标题`<h1>` -- `#`
    2. 二级标题`<h2>` -- `##`
    3. 三级标题`<h3>` -- `###`
    4. 四级标题`<h4>` -- `####`
    5. 五级标题`<h5>` -- `#####`
    6. 六级标题`<h6>` -- `######`

##区块引用

在每行前面加上`>`，如:

    > 这是区块引用第一行
    > 第二行
    > etc.

##列表

####无序列表

    * item 1
    * item 2
    * item 3

<em>注：`\*`可替换为`+`或`-`</em>

####有序列表

    1. item 1
    2. item 2
    3. item 3

##代码块

####缩进4个空格或一个Tab制表符

    def func():
        pass

####使用单撇号(\`)

如`` `代码在这` ``

##强调

1. **加粗**

    `**内容**`

2. *斜体*

    `*内容*`

> `*`可以用`_`替换

##超链接

####行内式:

    这是[谷歌](http://www.google.com，"可选的title")的链接

####参考式:

    这是[谷歌][id]的链接

    [id]: http://www.google.com "可选的title"

*注：同HTML一样、超链接可以是锚点*

##图片

同样分`行内式`和`参考式`，在此只写出行内式

    ![图片的替代文字](图片链接, "可选title")

##转义字符

同C语言一样，为` \ `


#参考链接

[Markdown语法说明（简体中文版）](http://wowubuntu.com/markdown/)
