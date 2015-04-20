---
layout: post
title: "模式识别——贝叶斯分类器"
date: 2015-04-20 16:03:42 +0800
comments: true
categories: 模式识别, 机器学习
---

贝叶斯分类器是一种原理简单、符合直觉但同时效果拔群的分类器，按照书上的划分，贝叶斯分类器有如下四种变体：

+ 最小错误率贝叶斯分类器（又称朴素贝叶斯分类器）
+ 最小风险贝叶斯分类器
+ 在限定一类错误率条件下另一类错误率最小贝叶斯分类器
+ 最小最大准则贝叶斯分类器

<!--more-->

贝叶斯分类器
==========

首先我们看一下最基本的条件概率公式：

$$ P(\boldsymbol{t}|w_i)P(w_i) = P(\boldsymbol{t}, w_i) = P(w_i| \boldsymbol{t})P(\boldsymbol{t}) $$

我们来解释一下这个公式：

+  $P(t|\boldsymbol{t})$ 代表当对象属于 $w_i$ 类时观测到的值为 $\boldsymbol{t}$ 的概率，即所谓的`先验概率`
+  $P(w_i|\boldsymbol{t})$ 代表当观测到的值是 $\boldsymbol{t}$ 时对象属于 $w_i$ 的概率。Bingo!既然要分类，我们要找的自然就是这个概率值，也就是所谓的`后验概率`
+ 其他的值 $P(w_i)$ 和 $P(\boldsymbol{t})$ 一目了然，自然不必多说

现在，我们对，条件概率公式进行变性，把我们想要的 $P(w_i|\boldsymbol{t})$ 分离出来，得到如下公式：

$$ P(w_i|\boldsymbol{t}) = \frac{P(\boldsymbol{t}|w_i)P(w_i)}{P(\boldsymbol{t})} $$

现在看看这个公式，它已经非常接近贝叶斯公式了（但还不是贝叶斯公式，不过已经可以用来分类了）。
如果我们要利用这个公式进行分类，我们需要知道其中的 $P(\boldsymbol{t}|w_i)P(w_i)$ 和 $P(w_i)$ ，好，假设我们知道了（别说我作弊、假设题设给出来了就OK）。

好，我们利用一下我们作为人类的直觉 —— 使 $P(w_i|\boldsymbol{t})$ 最大的 $i$ 就是观测值 $\boldsymbol{t}$ 的概率（基本等于废话）。同时我们应该注意到，$P(\boldsymbol{t})$ 与 $i$ 无关，所以我们的分类问题变成了如下一个以$i$为参数的问题：

$$ \arg\max_{i} P(\boldsymbol{t}|w_i)P(w_i) $$

这样，就形成了一个朴素贝叶斯分类器！

**注意，在这里我们的 $P(\boldsymbol{t}|w_i)P(w_i)$ 和 $P(w_i)$ 已知，比如 $P(w_1) =0.6$ 、 $P(\boldsymbol{t}|w_i)P(w_i)$ 是某个参数已知的正态分布**

代码
====

```python
import numpy as np

class PrimeBayesClassifier:
    """
    最小错误率贝叶斯分类器（又名朴素贝叶斯分类器）
    """
    
    def __init__(self, classes):
        """
        初始化函数，初始化先验概率及分布函数
        :param classes: 一个列表，每个元素代表一种类别，形式为一个元组(该类别先验概率，该类别分布函数）
        """
        self.classes = classes

    def classify(self, x):
        """
        分类函数
        :param x: 观察向量
        :return: 类别j
        """

        # p_w_t = P(w|t)
        # p_w = P(w)
        # p_t_w = P(t|w)
        p_w_t = [ (p_w * p_t_w(x)) for p_w, p_t_w in self.classes ]
        return np.argmax(p_w_t)
```

贝叶斯公式
========

现在，我们讨厌的产品经理需要我们加一个功能，即不光输出分类结果，还要输出 $P(w_i|\boldsymbol{t})$ 的值，那该怎么办呢？

现在我们引进全概率公式：

$$ P(\boldsymbol{t}) = \sum_{i=0}^{N}P(\boldsymbol{t}|w_i)P(w_i) $$

这样我们就算出来 $P(\boldsymbol{t})$ 了，我们将全概率公式带入上一节的公式中得到：

$$ P(w_i|\boldsymbol{t}) = \frac{P(\boldsymbol{t}|w_i)P(w_i)}{\sum_{i=0}^{N}P(\boldsymbol{t}|w_i)P(w_i)} $$

Bingo!上式就是我们神奇的贝叶斯公式了，式中的每一项都是知道的，最后我们就能算出来后验概率的值了，问题就这么解决了！至于代码，稍微改动一点就OK，我就懒得写了。

先验概率哪来的？！
==============

现在我们回到第一节遗留的一个问题 ——  $P(\boldsymbol{t}|w_i)P(w_i)$ 和 $P(w_i)$ 是咋来的，最简单的方法当然是*题设/老师/某砖家*告诉我们的。但是现实往往很残酷，我们能拿到的仅仅是一堆统计数据而已，那我们如何从大量的统计数据中发现 $P(\boldsymbol{t}|w_i)P(w_i)$ 和 $P(w_i)$ 这两个概率分布呢？这就是所谓的**机器学习**和**大数据**了。

而让机器从数据中学习到 $P(\boldsymbol{t}|w_i)P(w_i)$ 和 $P(w_i)$ 两个概率分布，也分两种情况：

+ 概率分布的形式已知，但参数未知（如未知参数的正态分布）
+ 分布形式也未知

问题一很好解决，我们有很多种方法，比如**最大似然估计**、**最小二乘估计**、**最小方差估计**、**卡尔曼滤波器**等等，都是经典统计学问题。

问题二的解决方法我目前只知道**Parzen窗算法**，以后再写吧。