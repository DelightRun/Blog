---
layout: post
title: "LaTeX笔记 —— 基础内容"
date: 2015-10-14 18:16:21 +0800
comments: true
categories: 
---

LaTeX学习过程中的一些笔记 —— 基础内容

<!-- more -->

## 文档类

### Usage:

    \documentclass[options]{class}

### Class:

+ `article` 排版科学期刊、演示文档、短报告、程序文档、邀请函......
+ `proc` 一个基于 article 的会议文集类
+ `minimal` 非常小的文档类。只设置了页面尺寸和基本字体。主要用来查错
+ `report` 排版多章节长报告、短篇书籍、博士论文......
+ `book` 排版书籍
+ `slides` 排版幻灯片。该文档类使用大号 sans serif 字体。也可以选用 FoilTEX来得到相同的效果。

### Options:

+ `10pt, 11pt, 12pt` 设置文档中所使用的字体的大小。如果该项没有指定,默认使用10pt 字体。+ `a4paper, letterpaper,` . . . 定义纸张的尺寸。缺省设置为letterpaper。此外,还可以使用a5paper, b5paper, executivepaper 以及legalpaper。+ `fleqn` 设置行间公式为左对齐,而不是居中对齐。+ `leqno` 设置行间公式的编号为左对齐,而不是右对齐。+ `titlepage, notitlepage` 指定是否在文档标题(document title) 后另起一 页。article 文档类缺省设置为不开始新页,report 和book 类则相反。+ `onecolumn, twocolumn` LATEX 以单栏(one column) 或双栏(two column) 的 方式来排版文档。+ `twoside, oneside` 指定文档为双面或单面打印格式。article 和report 类 为单面(single sided) 格式,book 类缺省为双面(double sided) 格式。注意 该选项只是作用于文档样式,而不会通知打印机以双面格式打印文档。+ `landscape` 将文档的打印输出布局设置为 landscape 模式。+ `openright, openany` 决定新的一章仅在奇数页开始还是在下一页开始。在文 档类型为article 时该选项不起作用,因为该类中没有定义“章” (chapter)。report 类默认在下一页开始新一章而book 类的新一章总是在 奇数页开始。

## 页面样式

### Usage:

全部设定：
    
    \￼pagestyle{style}
    
仅设置本页：

    ￼\thispagestyle{style}
    
### Style:
+ `￼plain` 在页脚正中显示页码。这是页面样式的缺省设置。+ `headings` 在页眉中显示章节名及页码,页脚空白。
+ `empty` 将页眉页脚都设为空白。

## 大型项目

### 引用单个文件

另起一页加入内容：

    \include{filename}

在当前位置插入文本：

    \input{filename}
    
### 进行语法差错而不生成

首先：

    \usepackage{syntonly}然后：    \syntaxonly
    
## 断行和分页

### 断行

另起一行而不另起一段：

    \\ 或 \newline
    
断行后禁止分页：

    \\*
    
### 分页

另起一页：

    \newpage
    
### 断词

设置断词点：

    \￼hyphenation{wo-rd1 w-or-d2}
    
命令
    
    \mbox{text}
    
保证把几个单词排在同一行上，其兄弟命令：

    \fbox{text}
    
还会额外围绕内容加个框

## 几个内置字符串

+ `\today`
+ `\TeX`
+ `\LaTeX`
+ `\LaTeXe`

## 特殊符号

### 引号

+ 左引号 —— 连续两个`` ` ``
+ 右引号 —— 连续两个`'`

### 破折号和连字号

+ `-` —— 连字号(hyphen)
+ `--` —— 短破折号(en-dash)
+ `---` —— 长破折号(em-dash)
+ `$-$` —— 负号/减号

### 波浪号

+ `\~{}` —— ` ̃`
+ `$\sim$` —— `∼`

### 度的符号

+ `\circ` —— `◦`

如果想排到右上角，可以如下：

    It’s $-30\,^{\circ}\mathrm{C}$
    
### 货币符号

首先载入宏包：

    \usepackage{textcomp}
    
然后引用：

+ `\texteuro` —— 欧元
+ `\textyen` —— 人民币
+ 其它符号请参考`textcomp`手册
    
### 省略号

+ `ldots`

## 交叉引用

+ `\label{marker}` —— 设定label
+ `\ref{marker}` —— 引用，序号
+ `\pageref{marker}` —— 引用，页号

## 脚注

### Usage:

    ￼\footnote{footnote text}
    
### Example:

    Footnotes\footnote{This is a footnote.} are often used by people using \LaTeX.## 强调

+ `\underline{text}` —— 下划线
+ `\emph{text}` —— 斜体

## 环境

### Usage:

    \begin{environment} TEXT \end{environment}
    
    
### 常用环境：

#### 列表:

+ `itemize` —— 无序列表
+ `enumerate` —— 有序列表
+ `description` —— 带描述的列表

Example:

```
\begin{enumerate}    \item You can mix the list environments to your taste:
        \begin{itemize}            \item But it might start to look silly.            \item[-] With a dash.        \end{itemize}    \item Therefore remember:
        \begin{description}            \item[Stupid] things will not become smart because they are in a list.            \item[Smart] things, though, can be presented beautifully in a list.        \end{description}\end{enumerate}
```

#### 左对齐、右对齐和居中

+ `flushleft` —— 左对齐
+ `flushright` —— 右对齐
+ `center` —— 居中

#### 引用、语录和韵文

+ `quote` —— 短引文、语录、例子
+ `quotation` —— 超过几段的长引文，会对段落进行缩紧
+ `verse` —— 用于诗歌

#### 摘要

+ `abstract` —— 就是论文的那个摘要

#### 原文打印

+ `verbatim` —— 原文打印，不执行中间的LaTeX命令

#### 表格

+ `tabular` —— 用法太麻烦了，不写了

#### 浮动体

就是浮动图片、图表什么的，使其周围被文本环绕

+ `figure` —— 图片
+ `table` —— 表格

可以带参数，如：

    \begin{figure}[arguments]

参数可以如下参数的组合：

+ `h` —— here 在文本的确切位置上,对于小的浮动体很有用。
+ `t` —— 在页面的顶部(top)
+ `b` —— 在页面的底部(bottom)
+ `p` —— 在一个只有浮动体的专门的页面(page) 上。
+ `!` —— 忽略阻止浮动体放置的大多数内部参数a。

此外，还可用如下命令添加说明文字：

    \caption[short]{long caption text}
    
## 保护脆弱命令

作为命令(如`\caption` 或`\section`)参量的文本,可能在文档中出现多次(例 如,在文档的目录和正文中)。当用于类似`\section`的参量时,一些命令会失效。它们被称为脆弱命令(fragile commands)。

`\footnote` 或`\phantom` 是脆弱命令的例子。这些脆弱命令需要的,正是保护。把`\protect` 命令放在它们前面, 就能保护它们。`\protect` 仅仅保护紧跟其右侧的命令,连它的参量也不惠及。在大多数情形下,过多的`\protect` 并不碍事。

### Example:

    \protect\footnote{and protect my footnotes}