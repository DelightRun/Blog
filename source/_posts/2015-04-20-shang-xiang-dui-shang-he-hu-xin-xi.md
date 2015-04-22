---
layout: post
title: "熵、相对熵和互信息"
date: 2015-04-20 19:56:13 +0800
comments: true
categories: 信息论, 熵
---

综述熵、相对熵和互信息的概念

<!--more-->

熵
===

**定义** 离散型随机变量X的`熵(entropy)` $H(X)$定义为：

$$ H(X) = -\sum_{x\in X}{p(x)\log{p(x)}} $$

> 注意：熵实际上是随机变量$X$概率分布的泛函

联合熵
=====

**定义** 对于服从联合分布为$p(x,y)$的一对离散型随机变量$(X,Y)$，其`联合熵(joint entropy)` $H(X,Y)$定义为：

$$ H(X,Y) = -\sum_{x\in X}{\sum_{y\in Y}{p(x,y)\log{p(x,y)}}} $$

亦可表示成：

$$ H(X,Y) = -E\log{p(X,Y)} $$

即一个随机变量在给定另一个随机变量下的`条件熵`，它是条件分布熵关于起条件作用的那个随机变量取平均后的期望值。

条件熵
=====

**定义** 若$(X,Y)$服从联合分布$p(x,y)$,`条件熵(conditional entropy)`$H(Y|X)$定义为：

$$ H(Y|X) = \sum_{x\in X}{p(x)H(Y|X=x)} = -\sum_{x\in X}{\sum_{y\in Y}{p(x,y)\log{p(y|x)}}} = -E_{p((x,y)}\log{p(Y|X)} $$

**定理**  `链式法则` 设随机变量$X_1,X_2,\cdots,X_n$服从$p(x_1,x2,\cdots,x_n)$，则有：

$$ H(X_1,X_2,\cdots,X_n) = \sum_{i=1}^{n}H(X_i|X_{i-1},\cdots,X_1) $$

比如，对于二元情况，$H(X,Y) = H(X) + H(Y|X)$


相对熵
=====

相对熵是两个随机分部之间的距离的度量。相对熵$D(p||q)$度量的是当真是分布为$p$而假定分布为$q$时的无效性。

**定义** 两个概率密度函数$p(x)$和$q(x)$之间的`相对熵`，或`Kullback Leibler距离`定义为：

$$ D(p||q) = \sum_{x\in X}{p(x)\log{\frac{p(x)}{q(x)}}} = E_p\log{\frac{p(X)}{q(X)}} $$

> 约定 $0\log{\frac{0}{q}}=0$ 和 $p\log{\frac{p}{0}}=\infty$ （基于连续性假设）

>注意，相对熵并不对称且不满足三角不等式，所以并不是`范数`，但是将其视作`距离`往往很有用


**定理** `相对熵的链式法则`

$$ D(p(x,y)||q(x,y)) = D(p(x)||q(x)) + D(p(y|x)||q(y|x)) $$


互信息
=====

**定义** 考虑两个随机变量$X$和$Y$，其联合概率密度函数为$p(x,y)$，其边际概率密度函数分别是$p(x)$和$p(y)$。`互信息`$I(X;Y)$定义为联合分布$p(x,y)$和乘积分布$p(x)p(y)$之间的相对熵，即：

$$ I(X;Y) = \sum_{x\in X}{\sum_{y\in Y}{p(x,y)\log{\frac{p(x,y)}{p(x)p(y)}}}} = D(p(x,y)||p(x)p(y)) = E_{p(x,y)}\log{\frac{p(X,Y)}{p(X)p(Y)}} $$

熵与互信息的关系
==============

注意到：

$$ I(X;Y) = H(X) - H(X|Y) = H(Y) - H(Y|X) $$

由此表明互信息I(X;Y)是在给定$Y(X)$知识条件下$X(Y)$的不确定度的缩减量，即$X(Y)$中含有$Y(X)$的信息量。

又因为$H(X,Y) = H(X) + H(Y|X)$，所以有：

$$ I(X;Y) = H(X) + H(Y) - H(X,Y) $$

最后，注意到：

$$ I(X;X) = H(X) $$

所以，有时熵也被称为`自信息(self-information)`。

综上，我们关于熵和互信息有如下一组定理公式

**定理** `互信息与熵`

$$ I(X;Y) = H(X) - H(X|Y) = H(Y) - H(Y|X) $$
$$ I(X;Y) = H(X) + H(Y) - H(X,Y) $$
$$ I(X;Y) = I(Y;X) $$
$$ I(X;X) = H(X) $$

条件互信息
=========

**定义** 随机变量$X$和$Y$在随机变量$Z$下的`条件互信息(conditional mutual information)`定义为：

$$ I(X;Y|Z) = H(X|Z) - H(X|Y,Z) = E_{p(x,y,z)}\log{\frac{p(X,Y|Z)}{p(X|Z)p(Y|Z)}} $$

**定理** `互信息链式法则`

$$ I(X_1,X_2,\cdots,X_n|Y) = \sum_{i=1}^{n}I(X_i;Y|X_{i-1},X_{i-2},\cdots,X_1) $$

条件相对熵
========

**定义** `条件相对熵(conditional relative entropy)`$D(p(y|x)||q(y|x))$定义为条件概率密度函数$p(y|x)$和$q(y|x)$之间的平均相对熵，其中“平均”二字是指针对$p(x)$平均，具体来讲就是：

$$ D(p(y|x)||q(y|x)) = \sum_{x}p(x)\sum_{y}p(y|x)\log{\frac{p(y|x)}{q(y|x)}} = E_{p(x,y)}\log{\frac{p(Y|X)}{q(Y|X)}} $$
