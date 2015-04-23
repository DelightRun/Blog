---
layout: post
title: "拉格朗日对偶性"
date: 2015-04-23 15:48:18 +0800
comments: true
categories: 机器学习, 数学
---

> 本文摘自：《统计学习方法》 李航. 清华大学出版社.

在约束最优化问题中，我们经常使用拉格朗日对偶性(Lagrange Duality)将原始问题转换为其对偶问题，通过解对偶问题而得到原始问题的解。

<!--more-->

原始问题
=======

假设$f(x)$,$c\_i(x)$,$h\_j(x)$是定义在$R^n$上的**连续可微函数**，则约束最优化问题表述如下：

$$\begin{equation} \min_{x\in R^n}{\;f(x)} \end{equation}$$

$$\begin{align}
s.t. \quad &c_i(x)\leq 0, \quad i=1,2,\cdots,k\\
&h_j(x) = 0, \quad j=1,2,\cdots,l
\end{align}$$

称此约束最优化问题为`原始最优化问题`或`原始问题`。

在此，我们引进`广义拉格朗日函数(generalized Lagrange function)`：

$$ L(x,\alpha,\beta) = f(x) + \sum_{i=1}^{k}{\alpha_i c_i(x)} + \sum_{j=1}^{l}{\beta_j h_j(x)} $$

这里，$x = (x\_1,x\_2,\cdots,x\_n)^T \in R^n$，$\alpha\_i$, $\beta\_i$是`拉格朗日乘子`, $\alpha_i \geq 0$。则考虑$x$的函数：

$$ \theta_P(x) = \max_{\alpha,\beta:\alpha_i \geq 0}{L(x,\alpha,\beta)} $$

这里的下标$P$表示原始问题。

现在，假设给定某个$x$。如果$x$违反原始问题的约束条件，即存在某个$i$使得$c\_i(x)>0$或存在某个$j$使得$h\_j(x) \neq 0$，那么就有：

$$ \theta_P(x) = \max_{\alpha,\beta:\alpha_i \geq 0}{\left[f(x) + \sum_{i=1}^{k}{\alpha_i c_i(x)} + \sum_{j=1}^{l}{\beta_j h_j(x)}\right]} = +\infty$$

相反地，如果$x$满足约束条件，则有$\theta_P(x) = f(x)$。因此：

$$ 
\theta_P(x) = 
\begin{cases}
f(x), & \text{x满足原始问题约束条件} \\
+\infty, & \text{其他} \\
\end{cases} 
$$

所以如果考虑极小化$\theta_P(x)$：

$$ \min_{x}{\theta_P(X)} = \min_{x}{\max_{\alpha,\beta:\alpha_i \geq 0}{L(x,\alpha,\beta)}} $$

它与原始最优化问题等价，即它们有相同的解。问题$\min\_{x}{\max\_{\alpha,\beta:\alpha\_i \geq 0}{L(x,\alpha,\beta)}}$称为`广义拉格朗如函数的极小极大问题`，这样我们就将原始问题转换成了广义拉格朗日函数的极小极大问题。为了方便，我们定义原始问题的最优值为：

$$ p^\ast = \min_{x}{\theta_P(x)} $$

对偶问题
=======

首先我们引入如下定义：

$$\theta_D(\alpha,\beta) = \min_{x}{L(x,\alpha,\beta)} $$

然后我们再考虑极大化$\theta_D(\alpha,\beta)=\min_{x}{L(x,\alpha,\beta)}$，即：

$$ \max_{\alpha,\beta:\alpha_i \geq 0}{\theta_D(\alpha,\beta)} = \max_{\alpha,\beta:\alpha_i \geq 0}{\min_{x}{L(x,\alpha,\beta)}} $$

上式问题称为`广义拉格朗日函数的极大极小问题`。

可以将广义拉格朗日函数的极大极小问题表示为约束最优化问题：

$$ \max_{\alpha,\beta}{\theta_D(\alpha,\beta)} = \max_{\alpha,\beta}{\min_{x}{L(x,\alpha,\beta)}} $$

$$ s.t. \quad \alpha_i \geq 0, i = 1,2,\cdots,k $$

上式所列约束最优化问题称为原始问题的`对偶问题`。定义对偶问题的最优值为：

$$ d^\ast = \max_{\alpha,\beta:\alpha_i \geq 0}{\theta_D(\alpha,\beta)} $$

原始问题与对偶问题的关系
====================

**定理1** 若原始问题与对偶问题都有最优值，则

$$ d^\ast = \max_{\alpha,\beta:\alpha_i \geq 0}{\min_{x}{L(x,\alpha,\beta)}} $$ 
$$ \leq $$
$$ \min_{x}{\max_{\alpha,\beta:\alpha_i \geq 0}{L(x,\alpha,\beta)}} = p^\ast $$

在某些条件下，原始问题与对偶问题的最优值相等，即$d^\ast = p^\ast$。这时我们可以用解对偶问题替代解原始问题。我们不加证明地叙述如下定理结论。

**定理2** 考虑原始问题和对偶问题。假设函数$f(x)$和$c\_i(x)$是凸函数，$h\_j(x)$是仿射函数（*即一阶多项式函数*$Ax+b$），并且假设不等式约束$c\_i(x)$是严格可行的（$\exists x\forall i \space c_i(x)<0$），则存在$x^\ast$,$\alpha^\ast$,$\beta^\ast$，使得$x^\ast$是原始问题的解，$\alpha^\ast$,$\beta^\ast$是对偶问题的解，并且

$$ p^\ast = d^\ast = L(x^\ast, \alpha^\ast, \beta^\ast) $$

**定理3** 对原始问题和对偶问题，假设函数$f(x)$和$c\_i(x)$是凸函数，$h\\_j(x)$是仿射函数，并且假设不等式约束$c\_i(x)$是严格可行的，则$x^\ast$和$\alpha^\ast$,$\beta^\ast$分别是原始问题和对偶问题的解的充分必要条件是$x^\ast$,$\alpha^\ast$,$\beta^\ast$满足如下**Karush-Kuhn-Tucker(KKT)条件**：

$$ \nabla_x L(x^\ast, \alpha^\ast, \beta^\ast) = 0 $$

$$ \nabla_\alpha L(x^\ast, \alpha^\ast, \beta^\ast) = 0 $$

$$ \nabla_\beta L(x^\ast, \alpha^\ast, \beta^\ast) = 0 $$

$$ \alpha_i^\ast c_i(x^\ast) = 0, \quad i = 1,2,\cdots,k $$

$$ c_i(x^\ast) \leq 0, \quad i = 1,2,\cdots,k $$

$$ \alpha_i^\ast \geq 0, \quad i = 1,2,\cdots,k $$

$$ h_j(x^\ast) = 0, \quad j = 1,2,\cdots,l $$

特别指出，$\alpha\_i^\ast c\_i(x^\ast) = 0$称为KKT的**对偶互补条件**。由此条件可知：**若$\alpha_i^\ast > 0$，则$c_i(x^\ast) = 0$**。