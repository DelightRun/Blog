---
layout: post
title: "反向传播方程组"
date: 2015-04-26 18:49:45 +0800
comments: true
categories: 机器学习, 神经网络 
---

反向传播算法的核心是通过`代价函数`计算出`权值`和`偏置`的改变量，即计算出$\frac{\partial C}{\partial w}$和$\frac{\partial C}{\partial b}$。

<!--more-->

## 反向传播方程组

$$
\begin{eqnarray}
\delta^L &=& \nabla_{a}{C} \odot \sigma'(z^L) \tag{BP1}\\
\delta^l &=& ((w^{l+1})^T \delta^{l+1}) \odot \sigma'(z^l) \tag{BP2}\\
\frac{\partial C}{\partial b^l} &=& \delta^l \tag{BP3}\\
\frac{\partial C}{\partial w^l} &=& (a^{l-1})^T \delta_j^l \tag{BP4}
\end{eqnarray}
$$

证明
===

#### 基本定义

+ $\sigma$是激活函数
+ $w$是链接权重，$b$是偏置

我们约定：

+ $w^L$、$b^L$表示从$L-1$层到$L$层的权重矩阵和偏置
+ $z^L$、$a^L$是$L$层的输出

然后我们有如下定义：

$$
\begin{eqnarray}
z^L &=& w^L a^{L-1} + b^L \tag{D1}\\
a^L &=& \sigma(z^L)   \tag{D2}\\
\delta^L &=& \frac{\partial C}{\partial z^L} \tag{D3}
\end{eqnarray}
$$

#### BP1与BP2的证明

由求导`链式法则`和方程式*D3*、*D2*，我们有：

$$\begin{eqnarray}
\delta^L &=& \frac{\partial C}{\partial z^L} \\
         &=& \frac{\partial C}{\partial a^L} \frac{\partial a^L}{\partial z^L} \\
         &=& \frac{\partial C}{\partial a^L} \sigma'(z^L) \\
         &=&\nabla_{a}{C} \odot \sigma'(z^L)
\end{eqnarray}$$

这样，我们就证明了*BP1*。同时，我们换种方式使用`链式法则`：

$$\begin{eqnarray}
\delta^l &=& \frac{\partial C}{\partial z^l} \\
         &=& \frac{\partial C}{\partial z^{l+1}} \frac{\partial z^{l+1}}{\partial z^l} \\
         &=& \delta^{l+1} \frac{\partial z^{l+1}}{\partial z^l} \\
         &=& \delta^{l+1} \frac{\partial (w^{l+1}\sigma(z^{l})+b^{l+1})}{\partial z^l}
         &=& \delta^{l+1} (w^{l+1}) \sigma'(z^l)
         &=& ((w^{l+1})^T \delta^{l+1}) \odot \sigma'(z^l)
\end{eqnarray}$$

#### BP3与BP4的证明

因为：

$$\begin{eqnarray}
z^{l}_j = \sum_k w^{l}_{jk} a^{l-1}_k + b^l_j
\end{eqnarray}$$

所以

$$\begin{eqnarray}
\frac{\partial C}{\partial b^l} &=& \frac{\partial C}{\partial z^l} \frac{\partial z^l}{\partial b^l} \\
&=& \delta^l
\end{eqnarray}$$

同理：

$$\begin{eqnarray}
\frac{\partial C}{\partial w_{jk}^l} &=& \frac{\partial C}{\partial z_j^l} \frac{\partial z_j^l}{\partial  w_{jk}^l} \\
&=& a_k^{l-1} \delta_j^l
&=& (a^{l-1})^T \delta_j^l
\end{eqnarray}$$