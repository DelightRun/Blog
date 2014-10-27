---
layout: post
title: 用Python写出仅需一行的快速排序
date: 2014-02-15 20:30:30 +0800
comments: true
categories: [Python]
---

作为一种非常常用的高效率排序算法，快速排序的算法思想却异常的简单，恐怕这便是所谓的**重剑无锋，大巧不工**。
虽然在C语言下快速排序算法比较长，并成为一些学渣在*数据结构*考试时的一个坎，但是如果使用*函数式语言*编写快速排序却只需一两行。

本文便是受*函数式编程*的启发，用Python写出一行的快速排序。
其实只要你理解了快排的思想，这个代码只能说是一个语法糖而已，没啥意思。

<!-- more -->

#预备知识

####lambda表达式
lambda表达式是`函数式编程`中的一种概念，也叫匿名函数。用法举例如下:

{% codeblock lang:python %}
f = lambda x: (x + 2) * x
print f(3) # => 15
{% endcodeblock %}

####列表推导式
Python中的列表推导式，这个自行[Google](https://www.google.com)吧，在Python中非常常用。

####Python中的三元表达式
在Python中也有三元表达式, 形式如下:

{% codeblock lang:python %}
TruePart if Condition else FalsePart
{% endcodeblock %}

相当于C语言中的:

{% codeblock lang:c %}
TruePart ? Condition : FalsePart
{% endcodeblock %}

#如何实现

我们知道，快排的思想是，选定一个`key`，然后将比`key`小的选出构成一个线性表`smaller`，比`key`大的也选出来构成一个线性表`bigger`，然后对`smaller`和`bigger`递归进行快排直到表为空，最后合并。
用Python表示就是:

{% codeblock lang:python %}
smaller = [i for i in data if i < key]
bigger = [i for i in data if i > key]
result = smaller + [key] + bigger
{% endcodeblock %}

那递归的边界条件怎么办呢？简单，用三元表达式啊:

{% codeblock lang:python %}
[] if len(X) == 0 else [doSomething]
{% endcodeblock %}

好了，现在再结合上lambda表达式，最后一行的快速排序如下:

{% codeblock lang:python %}
QuickSort = lambda X: [] if len(X) == 0 else QuickSort([i for i in X if i < X[0]]) + [X[0]] + QuickSort([i for i in X if i > X[0]])
{% endcodeblock %}

这就结束了，亲测可用。

#结语

很显然这样的快速排序是效率低下的，而且玩这种语法糖也没啥意思。但是当写出这句一行的的快速排序后，我瞬间明白了快速排序的原理。就当闲的没事娱乐下吧！
