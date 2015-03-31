---
layout: post
title: "面向对象的C编程"
date: 2015-03-31 19:25:38 +0800
comments: true
categories: C
---

> 翻译自[C Object Oriented Programming](http://nullprogram.com/blog/2014/10/21/)

<!--more-->

面向对象编程，尤其是多态性，对大型复杂软件的开发至关重要。
没有面向对象编程，则分离不同系统组件将是非常困难的。
C语言并不支持面向对象，所以大型C程序总是发展其自己的构建方式，
而不是单纯地依照原始的C语言准则。
比较有代表性的大型C语言项目的例子如Linux内核、BSD内核和SQLite

一个简单的例子
=============

假设你打算写一个函数`pass_match()`，该函数接受一个输入流、一个输出流和一个模式串。
这个函数的工作有点像`grep`命令，它将输入流中与模式串相匹配的行输出至输出流。
模式串是一个shell风格Glob模式串，该串与[POSI fnmath()](http://man7.org/linux/man-pages/man3/fnmatch.3.html)函数的模式串语法一致。
整个函数接口如下：

{% codeblock lang:c %}
void pass_match(FILE *in, FILE *out, const char *pattern);
{% endcodeblock %}

Glob风格模式串非常简单，所以不需要进行预编译（正则表达式一般需要预编译）。

一段时间后，我们的客户想让程序除了shell风格Glob字符串外还支持正则表达式。
为了性能需要，正则表达式需要被预编译，所以不能直接作为模式串传递给我们的函数，取而代之的将是一个[POSIX regex\_t](http://man7.org/linux/man-pages/man3/regexec.3.html)对象。
对本问题，一种快速但不怎么优雅的实现如下

{% codeblock lang:c %}
void pass_match(FILE *in, FILE *out, const char *pattern, regex_t *re);
{% endcodeblock %}

需要注意的是，`pattern`和`re`参数总有一个会是NULL。不过这个实现非常丑陋而且不便于扩展。
试想，如果我们需要更多种不同的匹配器该怎么办？所以我们需要一种只接受一个对象的实现，而不是像现在这样同时存在`pattern`和`re`对象。如果可能，我们还希望我们的对象可以扩展以适应各种不同的匹配器。

支持通用的匹配函数
=================

一种常见的用于扩展C语言函数的方式是向函数传递函数指针。
例如，作为比较器的`qsort()`函数的最后一个变量就是一个函数指针。

对于我们的`pass_match()`函数，这个函数指针指向的函数应该可以接受一个字符串并返回一个布尔值以表明该字符串是否该被我们的`pass_match()`函数传递至输出流。
我们对输入流的每一行调用该函数。

{% codeblock lang:c %}
void pass_match(FILE *in, FILE *out, bool (*match)(const char *));
{% endcodeblock %}

不过，这种实现同`qsort()`一样——缺乏上下文环境。`match`所指向的函数需要一个模式串或者一个`regex_t`对象来操作。在其他语言中，这种对上下文环境的依赖可以作为一个闭包附加到函数，但是C语言并不支持闭包。一种简单粗暴地实现方式是使用全局变量，但这并不值得提倡。

{% codeblock lang:c %}
static regexi_t regex;    // 非常差的方式！

bool regex_match(const char *string)
{
    return regexec(&regex, string, 0, NULL, 0) == 0;   
}
{% endcodeblock %}

因为全局变量的存在，`pass_match()`既不是可重入的也不是线程安全的。
我们将学习GNU的`qsort_r()`函数，接受一个上线文变量给我们的匹配函数，类似于一个闭包。

{% codeblock lang:c %}
void pass_match(FILE *in, FILE *out, 
        bool (*match)(const char *, void *), void *context);
{% endcodeblock %}

其中context指针将作为匹配函数的第二个参数以用来给其提供上下文环境，因此我们就用不到全局变量了。
这种实现对于许多简单情况是足够用了，我们的`pass_match()`接口也可以处理不同匹配函数的情况。

但是，我们为何不能将一个函数及其上下文环境打包为一个对象呢？

更抽象的做法
===========

**未完待续**
