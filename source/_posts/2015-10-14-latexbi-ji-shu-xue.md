---
layout: post
title: "LaTeX笔记 —— 数学"
date: 2015-10-14 20:19:45 +0800
comments: true
categories: 
---

LaTeX学习过程中的一些笔记 —— 数学相关

<!-- more -->

## 数学模式

### 行内模式

    $\lim_{n \to \infty}\sum_{k=1}^n \frac{1}{k^2}= \frac{\pi^2}{6}$
    
效果如下：

$\lim_{n \to \infty}\sum_{k=1}^n \frac{1}{k^2}= \frac{\pi^2}{6}$

### 普通模式

```
\begin{math}
\lim_{n \to \infty}\sum_{k=1}^n \frac{1}{k^2}= \frac{\pi^2}{6}
\end{math}
```

效果如下：

$$
\lim_{n \to \infty}\sum_{k=1}^n \frac{1}{k^2}= \frac{\pi^2}{6}
$$

### 在段落外显示

+ `\[ TEXT \]`
+ `\begin{displaymath} TEXT \end{displaymath}`

### 与文本模式的区别

1. 大多数的空格和断行没有任何意义,而且所有的空隙要么是从相应数学 表达式中自然的生成,要么是用一些专门的命令来指定,如`\,`(小空白), `\quad`(中等空白) 或`\qquad`(大空白)。
2. 空白行是不允许的。每个公式只能为一段。
3. 每一个字母都会被认为是一个变量名,且会相应被排版为此种样式。如果 你想要在公式中排版普通的文本(直立字体和普通字距),那么你必须要 把这些文本放在\textrm{...} 命令中。

## 方程和数组

### 方程

```
\begin{equation}
    \label{maker} EQUATION
\end{equation}
```

其中`\label`是可选的，为了给方程加上编号以方便`\ref`等的引用

### 数组

```
\begin{array}
    x_{11} & x_{12} & \ldots \\    x_{21} & x_{22} & \ldots \\    \vdots & \vdots & \ddots
\end{array}
```

## 对齐

使用`&`作为铆点进行对齐。

Example:

```
    a^2 + b^2 & = & c^2
    a & = & b
```
则对齐两个方程的等号

## 各种希腊字母、数学符号等

这就不多说了，查手册就行，而且还有各种LaTeX的App可供参考

## 复杂表达式中指标的放置

主要有两个环境：

+ substack环境 —— 居中对齐
+ subarray环境 —— 左对齐

```
\sum_{\substack{0<i<n \\ 1<j<m}}   P(i,j) =\sum_{\begin{subarray}{l}        i\in I \\ 1<j<m      \end{subarray}}
   Q(i,j)
```

## 定界符尺寸匹配

主要通过在定界符左边放置**成对的**如下两个命令实现：

+ `\left`
+ `\right`

Example:

$$ 1 + \left( \frac{1}{ 1-x^{2} } \right) $$

在必要的时候还可以通过如下四个命令调整尺寸：

+ `\big`
+ `\Big`
+ `\bigg`
+ `\Bigg`

Example：

    \Bigg( \bigg( \Big( \big( \big) \Big) \bigg) \Bigg)

效果如下：

$$ \Bigg( \bigg( \Big( \big( \big) \Big) \bigg) \Bigg) $$

## 虚位

可以通过`\phantom`命令为不存在的字符留下虚位，如下面这个例子：

```
{}^{12}_{\phantom{1}6}\textrm{C} 
   \qquad \textrm{VS} \qquad
{}^{12}_{6}\textrm{C}
```

左边的使用了虚位，右边的没有使用虚位，效果如下：

$$ 
{}^{12}_{\phantom{1}6}\textrm{C} 
   \qquad \textrm{VS} \qquad
{}^{12}_{6}\textrm{C}       
$$

## 定理、定律……

### Usage:

    ￼\newtheorem{name}[counter]{text}[section]

参量name 是用来标识“定理”的短关键字。而参数text 才是真正的“定理”名,它会在最终的文档中被打印出来。方括号中是可选参量。两者都均用来指定“定理”的编号问题。使用counter参数来指定先前声明的“定理”的name。则此新的“定理”将与先前定理统一编 号。section 参数让你来指定章节单元,而“定理”会按相应的章节层次来编号。

在你的文档的导言区执行\newtheorem 命令后,你就可以在文档中使用以下命令了。

```
\begin{name}[text]This is my interesting theorem 
\end{name}
```

### 样式

使用如下命令设置定理样式：

    \theoremstyle{style}
    
其中style有如下三种：

+ `definition` —— 标题粗体, 内容罗马体
+ `plain` —— 标题粗体,内容斜体
+ `remark` —— 标题斜体,内容罗马体

### Example

首先定义定理环境：

```
\theoremstyle{definition} \newtheorem{law}{Law}\theoremstyle{plain}      \newtheorem{jury}[law]{Jury}\theoremstyle{remark}     \newtheorem*{marg}{Margaret}
```

然后在文中写定理：

```
\begin{law} \label{law:box}Don’t hide in the witness box\end{law}\begin{jury}[The Twelve]It could be you! So beware andsee law \ref{law:box}\end{jury}\begin{marg}No, No, No\end{marg}
```

### 定理的证明

使用`proof`环境即可为定理写写证明

使用`\qedhere`表明证明完毕