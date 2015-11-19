---
layout: post
title: "矩阵论——范数理论"
date: 2015-11-11 15:08:06 +0800
comments: true
categories: [Math, Linear Algebra, Matrix Theory]
---

不加证明地简述向量范数和矩阵范数的概念与部分定理。

> 内容摘录自《矩阵论简明教程》（科学出版社）

<!-- more -->

# 向量范数

## 向量范数三公理

**定义** &nbsp; 若对任意 $$\boldsymbol{x} \in \mathbf{C}$$ 都有一个实数$$\|\boldsymbol{x}\|$$与之对应，且满足：

1. 非负性：当$\boldsymbol{x} \neq 0$时，$$\| \boldsymbol{x} \| \gt 0$$，当$\boldsymbol{x} = 0$时，$$\| \boldsymbol{x} \| = 0$$，
2. 齐次性：对任何$\lambda \in \mathbf{C}$，$$ \|\lambda \boldsymbol{x}\| = \vert\lambda\vert \|\boldsymbol{x}\| $$，
3. 三角不等式：对任意$\boldsymbol{x}, \boldsymbol{y} \in \mathbf{C}^n$，都有$$\| \boldsymbol{x} + \boldsymbol{y} \| \leq \| \boldsymbol{x} \| + \| \boldsymbol{y} \| $$，

则称$\\| \boldsymbol{x} \\|$为$\mathbf{C}^n$**上向量$\\| \boldsymbol{x} \\|$的范数，简称向量范数**。

## 常用向量范数

### 定义

设向量$$\boldsymbol{x} = (\xi_1, \xi_2, \cdots, \xi_n)^T \in \mathbf{C}^n$$

+ 向量**1范数**：

$$ \| \boldsymbol{x} \|_1 = \sum_{k=1}^{n}{\vert \xi_k \vert} $$

+ 向量**p范数**：

$$ \| \boldsymbol{x} \|_p = ( \sum_{k=1}^{n}{\vert \xi_k \vert^p} )^{\frac{1}{p}} \quad (1 \leq p \lt +\infty) $$

+ 向量**$\infty$范数**：

$$ \| \boldsymbol{x} \|_\infty = \max_{k}\vert \xi_k \vert $$

+ 向量**加权范数**或**椭圆范数**：

$$ \|\boldsymbol{x}\|_\boldsymbol{A} = \sqrt{\boldsymbol{x}^H\boldsymbol{A}\boldsymbol{x}}，\boldsymbol{A}是n阶Hermite正定矩阵 $$


### 性质

1. 常见的**1范数和2范数（欧氏距离）**是都是特殊的**p范数**
2. $$ \lim_{p \rightarrow +\infty} \|\boldsymbol{x}\|_p = \|\boldsymbol{x}\|_\infty $$
3. **2范数**具有**酉不变性**

## 向量范数等价性

**定义** &nbsp; 设 $$\| \bullet \|_a$$ 和 $$\| \bullet \|_b$$ 是 $\mathbf{C}^n$上的两种向量范数，如果存在**正数** $\alpha$ 和 $\beta$，使对任意 $\boldsymbol{x} \in \mathbf{C}^n$ 都有

$$ \alpha\|\boldsymbol{x}\|_a \leq \|\boldsymbol{x}\|_a \leq \beta\|\boldsymbol{x}\|_b $$

则称向量范数 $$\| \bullet \|_a$$ 和 $$\| \bullet \|_b$$ **等价**。

**定理** &nbsp; $\mathbf{C}^n$上所有向量范数等价

## $\boldsymbol{H\ddot{o}lder}不等式$

对任意 $$\xi_k, \eta_k \in \mathbf{C}(k=1,2,\cdots,n)$$，有：

$$ \sum_{k=1}^{n}{\vert \xi_k \vert \vert \eta_k \vert} \leq
    ( \sum_{k=1}^{n}{\vert \xi_k \vert^p} )^{\frac{1}{p}}
    ( \sum_{k=1}^{n}{\vert \eta_k \vert^q} )^{\frac{1}{q}} $$

其中 $p \gt 1, q \gt 1, \frac{1}{p} + \frac{1}{q} = 1$

> 当 $p = q = 2$ 时，即得到Cauchy-Schwarz不等式

# 矩阵范数

## 矩阵范数四公理

**定义** &nbsp; 若对任意 $\boldsymbol{A} \in \mathbf{C}^{m \times n}$ 都有一个实数 $\|\boldsymbol{A}\|$ 与之对应，且满足

1. 非负性：当 $\boldsymbol{A} \neq \boldsymbol{O}$ 时，$$\|\boldsymbol{A}\| \gt 0$$，当 $\boldsymbol{A} = \boldsymbol{O}$ 时，$$\|\boldsymbol{A}\| = 0$$，
2. 齐次性：对任意 $$\lambda \in \mathbf{C}， \|\lambda \boldsymbol{A}\| = \vert\lambda \vert \| \boldsymbol{A} \|$$，
3. 三角不等式：对任意 $\boldsymbol{A,B} \in \mathbf{C}^{n \times n}$，都有 $$\|\boldsymbol{A} + \boldsymbol{B}\| \leq \|\boldsymbol{A}\| + \|\boldsymbol{B}\|$$，
4. 相容性：对任意 $\boldsymbol{A} \in \mathbf{C}^{m \times n}, \boldsymbol{B} \in \mathbf{C}^{n \times l}$，都有 $$\|\boldsymbol{A}\boldsymbol{B}\| \leq \|\boldsymbol{A}\| \|\boldsymbol{B}\|$$，

则称 $$\| \boldsymbol{A} \|$$ 为 $\mathbf{C}^{m \times n}$**上矩阵 $\boldsymbol{A}$ 的范数，简称矩阵范数**。

## 与向量范数的相容性

**定义** &nbsp; 设 $$\| \bullet \|_m$$ 是 $\mathbf{C}^{n \times n}$ 上的矩阵范数，$$\| \bullet \|_v$$ 是 $\mathbf{C}^n$ 上的向量范数，如果对任意 $\boldsymbol{A} \in \mathbf{C}^{n \times n}$ 和 $\boldsymbol{x} \in \mathbf{C}^m$ 都有

$$ \|\boldsymbol{A}\boldsymbol{x}\|_v \leq \|\boldsymbol{A}\|_m \|\boldsymbol{x}\|_v $$

则称矩阵范数 $$\| \bullet \|_m$$ 与向量范数 $$\| \bullet \|_v$$ 是**相容**的。

## 从属范数（又名：导出范数）

我们知道，单位矩阵在矩阵乘法中的作用类似于1在数的乘法的作用，但是对于矩阵的$m_1$、F和M范数，有

$$ \|\boldsymbol{I}_n\|_{m_1} = n, \quad \|\boldsymbol{I}_n\|_F = \sqrt{n}, \quad \|\boldsymbol{I}_n\|_M = n $$

这对于一些理论分析带来不便，因此下面定理告诉我们如何构造出使$\| \boldsymbol{I}_n \| \equiv 1$的矩阵范数。

**定理** &nbsp; 已知 $\mathbf{C}^n$ 上的向量范数 $$\| \bullet \|_v$$，对任意 $\boldsymbol{A} \in \mathbf{C}^{m \times n}$，规定

$$ \| \boldsymbol{A} \| = \max_{x \neq 0}{\frac{\|\boldsymbol{A} \boldsymbol{x}\|_v}{\| \boldsymbol{x} \|_v}}  = \max_{\| \boldsymbol{X} \|_v = 1}{\| \boldsymbol{A} \boldsymbol{x} \|_v} $$

则 $$\| \bullet \|$$ 是 $\mathbf{C}^{m \times n}$上与向量范数 $$\| \bullet \|_v$$ 相容的矩阵范数，称之为**由向量范数 $$\| \bullet \|_v$$ 导出的矩阵范数**或**从属于向量范数 $$\| \bullet \|_v$$ 的矩阵范数**，简称**导出范数**或**从属范数**。

## 常用矩阵范数

设 $$\boldsymbol{A} = (a_{ij})_{m \times n} \in \mathbf{C}^{m \times n}$$

+ 矩阵$\boldsymbol{m\_1}$**范数**：

$$ \| \boldsymbol{A} \|_{m_1} = \sum_{i=1}^{m}{\sum_{j=1}^{n}{\vert a_{ij} \vert}} $$

+ 矩阵**Frobeniuse范数**或**F范数**：

$$ \| \boldsymbol{A} \|_F = \sqrt{ \sum_{i=1}^{m}{\sum_{j=1}^{n}{\vert a_{ij} \vert^2 }} } = \sqrt{tr(\boldsymbol{A}^H \boldsymbol{A})}$$

+ 矩阵**M范数**或**最大范数**：

$$ \| \boldsymbol{A} \|_M = max\{m,n\} \max_{i,j}{\vert a_{ij} \vert} $$

+ 矩阵**G范数**或**几何平均范数**：

$$ \| \boldsymbol{A} \|_G = \sqrt{mn} \max_{i,j}{\vert a_{ij} \vert} $$

+ 矩阵**1范数**或**列和范数**：

$$ \| \boldsymbol{A} \|_1 = \max_{j}{\sum_{i=1}^{m}{\vert a_{ij} \vert}} $$

+ 矩阵**2范数**或**谱范数**：

$$ \| \boldsymbol{A} \|_2 = \sqrt{\boldsymbol{A}^H \boldsymbol{A} 的最大特征值} $$

+ 矩阵$\boldsymbol{\infty}$**范数**或**行和范数**：

$$ \max_i{\sum_{j=1}^{n}{\vert a_{ij} \vert}} $$

### 性质

1. **F范数**和**2范数**具有`酉不变性`
2. 相容性：
    + **矩阵$m\_1$范数**与**向量1范数**相容
    + **矩阵F范数、G范数**与**向量2范数**相容
    + **矩阵M范数**分别与**向量1、2、$\boldsymbol{\infty}$范数**相容
    +  **矩阵1、2、$\boldsymbol{\infty}$范数**分别与**向量1、2、$\boldsymbol{\infty}$范数**相容
3. **矩阵1、2、$\boldsymbol{\infty}$范数**分别由**向量1、2、$\boldsymbol{\infty}$范数**导出，从而与相应的向量范数相容

# 计算范数的Matlab命令 —— norm

> 在Matlab中使用`doc norm`可查看其文档，在此不再赘述

# 范数的两种常见应用

## 谱半径

**定义** &nbsp; 设 $$\boldsymbol{A} \in \mathbf{C}^{n \times n}, \lambda_1, \lambda_2, \cdots, \lambda_n$$ 为 $\boldsymbol{A}$ 的 $n$ 个特征值，称

$$ \rho(\boldsymbol{A}) = \max_{j}{\vert \lambda_j \vert} $$

为 $\boldsymbol{A}$ 的**谱半径**

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{n \times n}$， 则

1. $\rho(\boldsymbol{A}^k) = (\rho(\boldsymbol{A}))^k$
2. $\rho(\boldsymbol{A}^H \boldsymbol{A}) = \rho(\boldsymbol{A} \boldsymbol{A}^H) = \\| \boldsymbol{A} \\|\_2^2$
3. 当 $\boldsymbol{A}$ 是正规矩阵时，$$\rho(\boldsymbol{A}) = \|A\|_2$$

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{n \times n}$， 则对 $\mathbf{C}^{n \times n}$上的任一矩阵范数 $$\| \bullet \|$$，都有

$$ \rho(\boldsymbol{A}) \leq \| \boldsymbol{A} \| $$

## 条件数

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}_n^{n \times n}$， $$\| \bullet \|$$ 是 $\mathbf{C}^{n \times n}$ 上的矩阵范数，称

$$ cond(\boldsymbol{A}) = \| \boldsymbol{A} \| \| \boldsymbol{A}^{-1} \| $$

为矩阵 $\boldsymbol{A}$（关于求逆或求解线性方程组）的**条件数**。

一般地，如果矩阵 $\boldsymbol{A}$ 的条件数大就称 $\boldsymbol{A}$ 对于求逆矩阵或求解线性方程组是**病态的**，或**坏条件的**；否则，称为**良态**或**好条件的**
