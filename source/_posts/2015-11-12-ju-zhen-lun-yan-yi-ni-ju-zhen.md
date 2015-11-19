---
layout: post
title: "矩阵论——广义逆矩阵"
date: 2015-11-12 16:42:02 +0800
comments: true
categories: [Math, Linearn Algebra, Matrix Theory]
---

给出广义逆矩阵的定义，并不假证明地给出几种常用广义逆矩阵。

> 内容摘自《矩阵论简明教程》（科学出版社）一书。

<!-- more -->

# 广义逆矩阵的概念

**定义** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}$。如果 $\boldsymbol{X} \in \mathbf{C}^{n \times m}$满足下列四个**Penrose方程**

1. $\boldsymbol{AXA} = \boldsymbol{A}$
2. $\boldsymbol{XAX} = \boldsymbol{X}$
3. $(\boldsymbol{AX})^H = \boldsymbol{AX}$
4. $(\boldsymbol{XA})^H = \boldsymbol{XA}$

的某几个或全部，则称 $\boldsymbol{X}$ 是 $\boldsymbol{A}$ 的**广义逆矩阵**。满足全部四个方程的广义逆矩阵 $\boldsymbol{X}$ 称为 $\boldsymbol{A}$ 的
**Moore-Penrose逆**。

> 显然，如果 $\boldsymbol{A}$ 是可逆矩阵，则 $\boldsymbol{X} = \boldsymbol{A}^{-1}$ 满足四个Penrose方程。

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}$，则 $\boldsymbol{A}$ 的Moore-Penrose逆存在且唯一。

> 注意：只要 $\boldsymbol{A}$ 不是可逆矩阵，则除了Moore-Penrose逆以外的其他14类广义逆矩阵都不是唯一的。

**定义** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}$。若 $\boldsymbol{X} \in \mathbf{C}^{n \times m}$ 满足Penrose方程中的第$(i),(j),\cdots,(l)$
等方程，则称 $\boldsymbol{X}$ 为 $\boldsymbol{A}$ 的 $\{\boldsymbol{i},\boldsymbol{j},\cdots,\boldsymbol{l}\}$ **逆**，记为 $$A^{(i,j,\cdots,l)}$$，
其全体记为$$\boldsymbol{A}\{i,j,\cdots,l\}$$。$\boldsymbol{A}$的唯一的Moore-Penrose逆记为 $\boldsymbol{A}^{+}$，也称之为 $\boldsymbol{A}$ 的**加号逆**。

# 由{1}逆构造其他广义逆矩阵

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}$，$\boldsymbol{Y}, \boldsymbol{Z} \in A\{1\}$，记 $\boldsymbol{X} = \boldsymbol{YAZ}$，则 $\boldsymbol{X} \in A\{1,2\}$

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}$，$$(\boldsymbol{A}^H\boldsymbol{A})^{(1)} \in (A^HA)\{1\}$$，$$(\boldsymbol{A}\boldsymbol{A}^H)^{(1)} \in (AA^H)\{1\}$$，则

$$ \boldsymbol{Y} = (\boldsymbol{A}^H\boldsymbol{A})^{(1)}\boldsymbol{A}^H \in A\{1,2,3\}, \quad \boldsymbol{Z} = \boldsymbol{A}^H(\boldsymbol{A}\boldsymbol{A}^H)^{(1)} \in A\{1,2,4\} $$

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}$，且$\mathbf{A}^{(1,3)} \in A\{1,3\}, \boldsymbol{A}^{(1,4)} \in A\{1,4\}$，则

$$ \boldsymbol{A}^{+} = \boldsymbol{A}^{(1,4)}\boldsymbol{A}\boldsymbol{A}^{(1,3)} $$

# Moore-Penrose逆$\boldsymbol{A}^{+}$

> Moore-Penrose逆毋庸置疑是所有矩阵广义逆中最重要的一种，因此下面我们给出它的性质、两种求法和在解方程中的重要应用

## 性质

设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}$，则

1. $(\boldsymbol{A}^{+})^{+} = \boldsymbol{A}$
2. $(\boldsymbol{A}^{+})^H = (\boldsymbol{A}^H)^{+}, (\boldsymbol{A}^{+})^T = (\boldsymbol{A}^T)^{+}$
3. $(\lambda\boldsymbol{A})^{+} = \lambda^{+}\boldsymbol{A}^{+}, \lambda \in \mathbf{C}$
4. $\operatorname{rank}{\boldsymbol{A}^{+}} = \operatorname{rank}{\boldsymbol{A}}$
5. $\operatorname{rank}{\boldsymbol{A}\boldsymbol{A}^{+}} = \operatorname{rank}{\boldsymbol{A}^{+}\boldsymbol{A}} = \operatorname{rank}{\boldsymbol{A}}$
6. $\boldsymbol{A}^{+} = (\boldsymbol{A}^H\boldsymbol{A})^{+}\boldsymbol{A}^H = \boldsymbol{A}^H(\boldsymbol{A}\boldsymbol{A}^H)^{+}$
7. $(\boldsymbol{A}^H\boldsymbol{A})^{+} = \boldsymbol{A}^{+}(\boldsymbol{A}^H)^{+}, (\boldsymbol{A}\boldsymbol{A}^H)^{+} = (\boldsymbol{A}^H)^{+}\boldsymbol{A}^{+}$
8. 当$\boldsymbol{U}$和$\boldsymbol{V}$分别是$m$阶和$n$阶酉矩阵时，有

$$ (\boldsymbol{UAV})^{+} = \boldsymbol{V}^H\boldsymbol{A}^{+}\boldsymbol{U}^H $$

9. $\boldsymbol{A}\boldsymbol{A}^{+} = \boldsymbol{I}\_m \Leftrightarrow \operatorname{rank}{\boldsymbol{A}} = m$
10. $\boldsymbol{A}^{+}\boldsymbol{A} = \boldsymbol{I}\_n \Leftrightarrow \operatorname{rank}{\boldsymbol{A}} = n$

## 两种常用算法

### 使用SVD

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}，\boldsymbol{b} \in \mathbf{C}^{m}$，且 $\boldsymbol{A}$ 的SVD为

$$ \boldsymbol{A} = \boldsymbol{U} \begin{pmatrix} \boldsymbol{\Sigma} & \boldsymbol{O} \\\ \boldsymbol{O} & \boldsymbol{O} \end{pmatrix} \boldsymbol{V}^H $$

则

$$ \boldsymbol{A}^{+} = \boldsymbol{V} \begin{pmatrix} \boldsymbol{\Sigma}^{-1} & \boldsymbol{O} \\\ \boldsymbol{O} & \boldsymbol{O} \end{pmatrix} \boldsymbol{U}^H $$

### 使用满秩分解

**定理**&nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}\_r(r \gt 0)$，且 $\mathbf{A}$ 的满秩分解为

$$ \boldsymbol{A} = \boldsymbol{FG} \quad (\boldsymbol{F} \in \mathbf{C}^{m \times r}_{r}, \boldsymbol{G} \in \mathbf{C}^{r \times n}_{r}) $$

则

$$ \boldsymbol{A}^{+} = \boldsymbol{G}^H(\boldsymbol{G}\boldsymbol{G}^H)^{-1}(\boldsymbol{F}^H\boldsymbol{F})^{-1}\boldsymbol{F}^H $$

## 通过Moore-Penrose逆解方程

设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}$，有线性方程组 $\boldsymbol{Ax} = \boldsymbol{b}$，则有如下结论：

1. $\boldsymbol{Ax} = \boldsymbol{b}$有解（相容） $\Leftrightarrow$ $\boldsymbol{AA}^{+}\boldsymbol{b} = \boldsymbol{b}$
2. $\boldsymbol{x} = \boldsymbol{A}^{+}\boldsymbol{b} + (\boldsymbol{I} - \boldsymbol{A}^{+}\boldsymbol{A})\boldsymbol{y} (\boldsymbol{y} \in \mathbf{C}^{n}任意)$是相容方程组
$\boldsymbol{Ax} = \boldsymbol{b}$的**通解**，或是矛盾方程组$\boldsymbol{Ax} = \boldsymbol{b}$的**全部最小二乘解**
3. $\boldsymbol{x}\_0 = \boldsymbol{A}^{+}\boldsymbol{b}$ 是相容方程组 $\boldsymbol{Ax} = \boldsymbol{b}$的**唯一极小范数解**，或是矛盾方程组$\boldsymbol{Ax} = \boldsymbol{b}$
的**唯一极小范数最小二乘解**

简而言之，我们始终可以通过：

$$ \boldsymbol{x}_0 = \boldsymbol{A}^{+}\boldsymbol{b} $$

来求线性方程组$\boldsymbol{Ax} = \boldsymbol{b}$的**唯一极小范数（最小二乘）解**。

## Matlab命令

    pinv

# Drazin逆
