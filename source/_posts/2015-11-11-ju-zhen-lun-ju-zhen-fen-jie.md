---
layout: post
title: "矩阵论——矩阵分解"
date: 2015-11-11 18:53:08 +0800
comments: true
categories: [Math, Linear Algebra, Matrix Theory]
---

不加证明地给出几种常用的矩阵分解

> 内容摘录自《矩阵论简明教程》（科学出版社）

<!-- more -->

# 三角分解

## 基本概念

**定义** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{n \times n}$。如果存在`下三角矩阵`$\boldsymbol{L} \in \mathbf{C}^{n \times n}$和`上三角矩阵`$\mathbf{R} \in \mathbf{C}^{n \times n}$，使得

$$ \boldsymbol{A} = \boldsymbol{LR} $$

则称 $\boldsymbol{A}$ 可以作**LU分解**或**三角分解**。

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{n \times n}\_n$，则 $\boldsymbol{A}$ 可作LU分解的**充分必要条件**是 $$\Delta_{k} \neq 0 (k = 1,2,\cdots,n-1)$$，其中$$\Delta_{k} = \det{\boldsymbol{A}_{k}}$$ 
为 $\boldsymbol{A}$ 的 $k$ 阶顺序主子式，而 $\boldsymbol{A}_k$ 为 $\boldsymbol{A}$ 的 $k$ 阶顺序主子阵。

> 这个定理说明，并不是每个可逆矩阵都可LU分解

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{n \times n}\_r$，且 $\boldsymbol{A}$ 的前 $r$ 个顺序主子式不为0，则 $\boldsymbol{A}$ 可作LU分解。

> 该定理的条件仅是充分的

**定义** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{n \times n}$

+ 如果 $\boldsymbol{A}$ 可分解成 $\boldsymbol{A} = \boldsymbol{LR}$，其中 $\boldsymbol{L}$ 是`单位下三角阵`，$\mathbf{R}$是`上三角阵`，则称之为 $\boldsymbol{A}$ 的**Doolittle分解**
+ 如果 $\boldsymbol{A}$ 可分解为 $\boldsymbol{A} = \boldsymbol{LR}$，其中 $\boldsymbol{L}$ 是`下三角阵`，$\mathbf{R}$是`单位上三角阵`，则称之为 $\boldsymbol{A}$ 的**Crout分解**
+ 如果 $\boldsymbol{A}$ 可分解为 $\boldsymbol{A} = \boldsymbol{LDR}$，其中 $\boldsymbol{L}$ 是`单位下三角阵`，$\boldsymbol{D}$是`对角矩阵`，$\mathbf{R}$是`单位上三角阵`，则称之为 $\boldsymbol{A}$ 的**LDR分解**

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{n \times n}\_n$，则 $\boldsymbol{A}$ 由唯一LDR分解的充分必要条件是 $$\Delta_{k} \neq 0 (k = 1,2,\cdots,n-1)$$。此时对角矩阵 $$\boldsymbol{D} = diag(d_1,d_2,\cdots,d_n)$$
的元素满足

$$ d_1 = \Delta_{1}, \quad d_k = \frac{\Delta_{k}}{\Delta_{k-1}} \quad (k = 2,3,\cdots,n) $$


**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{n \times n}\_n$，则 $\boldsymbol{A}$ 可作Doolittle分解或Crout分解的**充分必要条件**是 $$\Delta_{k} \neq 0 (k = 1,2,\cdots,n-1)$$。

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{n \times n}$ 是Hermite正定矩阵，则存在下三角矩阵 $\boldsymbol{G} \in \mathbf{C}^{n \times n}$ 使得

$$ \boldsymbol{A} = \boldsymbol{G} \boldsymbol{G}^H $$

称之为 $\boldsymbol{A}$ 的**Cholesky分解**，或写成LDR分解形式

$$ \boldsymbol{A} = \boldsymbol{L} \boldsymbol{D} \boldsymbol{L}^H $$

称之为 $\boldsymbol{A}$ 的**LDL分解**

## Matlab程序

> 在此只列出命令名字，请参考Matlab文档使用 —— `doc 命令名字`

### LU分解

    lu

### Cholesky分解

    chol

### LDL分解

    ldl

### LDR分解

```matlab
function [L, D, R] = LDR(A)
[m, n] = size(A)    % 获取矩阵行数m和列数

% 判断矩阵是否为方阵
if (m ~= n)
    error('非方阵，不可分解')
end

% 判断矩阵是否可逆
if (n ~= rank(A))
    errror('奇异矩阵，不可分解')
end

% 判断矩阵是否有唯一LDR分解
for k = 1:n-1
    D(k) = det(A(1:k, 1:k));
    if (D(k) == 0)
        error(sprintf('%d阶顺序主子式为0，分解不唯一', k))
    end
end

% 算法见《矩阵论简明教程》p89 定理4.3之证明
[L, R] = lu(A);     % 对A做LU分解
DL = diag(diag(L));
DR = diag(diag(R));
L = L * inv(DL);
D = DL * DR;
R = inv(DR) * R;
end
```

### Doolittle分解

    TODO：Doolittle分解的程序

### Crout分解

    TODO：Crout分解的程序

# QR分解

## Householder矩阵和Givens矩阵

### Householder矩阵

#### 定义与性质

**定义** &nbsp; 设 $\boldsymbol{u} \in \mathbf{C}^{n}$ 是单位向量，即 $\boldsymbol{u}^H \boldsymbol{u} = 1$，称

$$ \boldsymbol{H} = \boldsymbol{I} - 2 \boldsymbol{u}\boldsymbol{u}^H $$

为**Householder矩阵**或**初等反射矩阵**。由Householder矩阵 $\boldsymbol{H}$ 确定的 $\mathbf{C}^n$ 上的线性变换
 $\boldsymbol{y} = \boldsymbol{H}\boldsymbol{x}$ 称为**Householder变换**或**初等反射变换**。

**性质** &nbsp; 设 $\boldsymbol{H} \in \mathbf{C}^{n \times n}$是Householder矩阵，则

1. $$\boldsymbol{H}^H = \boldsymbol{H}$$（Hermite矩阵）
2. $$\boldsymbol{H}^H \boldsymbol{H} = \boldsymbol{I}$$（酉矩阵）
3. $$\boldsymbol{H}^2 = \boldsymbol{I}$$（对合矩阵）
4. $$\boldsymbol{H}^{-1} = \boldsymbol{H}$$（自逆矩阵）
5. $$\begin{pmatrix} \boldsymbol{I_r} & \boldsymbol{O} \\\ \boldsymbol{O} & \boldsymbol{H} \end{pmatrix}$$是$n+r$阶Householder矩阵
6. $\det{\boldsymbol{H}} = -1$

#### 重要定理

**定理** &nbsp; 设 $\boldsymbol{z} \in \mathbf{C}^n$ 是单位向量，则对任意 $\boldsymbol{x} \in \mathbf{C}^n$，
存在Householder矩阵 $\boldsymbol{H}$，使得 $\boldsymbol{H}\boldsymbol{x} = \alpha\boldsymbol{z}$，其中$\vert \alpha \vert
 = \\| \boldsymbol{x} \\|\_2$，且 $\alpha\boldsymbol{x}^H\boldsymbol{z}$ 为实数。

上述定理中 $\boldsymbol{H}$ 构造方法如下：

+ 当 $\boldsymbol{x} = 0$ 时，任取单位向量$boldsymbol{u}$
+ 当 $\boldsymbol{x} = \alpha\boldsymbol{z} \neq 0$ 时，取单位向量$\boldsymbol{u}$满足$\boldsymbol{u}^H\boldsymbol{x} = 0$
+ 当 $\boldsymbol{x} \neq \alpha\boldsymbol{z}$ 时，取

$$ \boldsymbol{u} = \frac{\boldsymbol{x} - \alpha\boldsymbol{z}}{\| \boldsymbol{x} - \alpha\boldsymbol{z} \|_2} $$

**推论1** &nbsp; 对任意 $\boldsymbol{x} \in \mathbf{C}^n$，存在Householder矩阵 $\boldsymbol{H} = \boldsymbol{I}-2\boldsymbol{u}\boldsymbol{u}^H$，
使得 $$\boldsymbol{H}\boldsymbol{x} = \alpha\boldsymbol{e}_1$$，其中$$\vert \alpha \vert = \|\boldsymbol{x}\|_2$$，
且$\alpha\boldsymbol{x}^H\boldsymbol{e}\_1$为实数。

**推论2** &nbsp; 对任意 $\boldsymbol{x} \in \mathbf{R}^n$，存在Householder矩阵$$ \boldsymbol{H} = \boldsymbol{I}-2\boldsymbol{u}\boldsymbol{u}^T$$，
使得 $\boldsymbol{H}\boldsymbol{x} = \alpha\boldsymbol{e}\_1$，其中$$\alpha=\pm \|\boldsymbol{x}\|_2$$。

### Givens矩阵

#### 定义

**定义** &nbsp; 设 $c, s \in \mathbf{C}$，且满足$$\vert c\vert^2 + \vert s\vert^2 = 1$$，称$n$阶矩阵

$$ \boldsymbol{T}_{pq} = \begin{pmatrix}
                          1 &        &   &          &   &         &   &          &   &        &   \\\
                            & \ddots &   &          &   &         &   &          &   &        &   \\\
                            &        & 1 &          &   &         &   &          &   &        &   \\\
                            &        &   & \bar{c}  &   &         &   & \bar{s}  &   &        &   \\\
                            &        &   &          & 1 &         &   &          &   &        &   \\\
                            &        &   &          &   & \ddots  &   &          &   &        &   \\\
                            &        &   &          &   &         & 1 &          &   &        &   \\\
                            &        &   &    -s    &   &         &   &     c    &   &        &   \\\
                            &        &   &          &   &         &   &          & 1 &        &   \\\
                            &        &   &          &   &         &   &          & 1 &        &   \\\
                            &        &   &          &   &         &   &          &   & \ddots & 1
                    \end{pmatrix}
$$

（$\bar{c}$ 位于$p$行$p$列，$c$ 位于$q$行$q$列）

为**Givens矩阵**或**初等旋转矩阵**。由Givens矩阵 $$\boldsymbol{T}_{pq}$$ 确定的 $\mathbf{C}^n$ 上的线性变换 
$$\boldsymbol{y} = \boldsymbol{T}_{pq} \boldsymbol{x}$$ 称为**Givens变换**或**初等旋转变换**。

#### 重要定理

**定理** &nbsp; 对任意 $$\boldsymbol{x} = (\xi_1,\xi_2,\cdots,\xi_n)^T \in \mathbf{C}^n$$，存在Givens矩阵 $$\boldsymbol{T}_{pq}$$，使得 $$\boldsymbol{T}_{pq}\boldsymbol{x}$$
的第$q$个分量为零，第$p$个分量为非负实数，其余分量不变。

上述定理中 $\boldsymbol{T}\_{pq}$ 的构造方法如下：

+ 当 $$\vert \xi_p \vert^2 + \vert \xi_q \vert^2 = 0$$ 时，取$c = 1, s = 0$，即 $$\boldsymbol{T}_{pq} = \boldsymbol{I}$$
+ 当 $$\vert \xi_p \vert^2 + \vert \xi_q \vert^2 \neq 0$$ 时，取

$$ c = \frac{\xi_p}{\sqrt{\vert \xi_p \vert^2 + \vert \xi_q \vert^2}}, \quad s = \frac{\xi_q}{\sqrt{\vert \xi_p \vert^2 + \vert \xi_q \vert^2}} $$


**推论** &nbsp; 设 $$\boldsymbol{x} = (\xi_1,\xi_2,\cdots,\xi_n)^T \in \mathbf{C}^n$$ ，则存在Givens矩阵 $$\boldsymbol{T}_{12},\boldsymbol{T}_{13},\cdots,\boldsymbol{T}_{1n}$$，使得

$$ \boldsymbol{T}_{1n}\cdots\boldsymbol{T}_{13}\boldsymbol{T}_{12}\boldsymbol{x} = \|\boldsymbol{x}\|_2 \boldsymbol{e}_1 $$

称之为用Givens变换化向量$\boldsymbol{x}$与$\boldsymbol{e}\_1$同方向。

## QR分解

**定义** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{n \times n}$，如果存在$n$阶酉矩阵$\boldsymbol{Q}$和$n$阶上三角矩阵$\mathbf{R}$，使得

$$ \boldsymbol{A} = \boldsymbol{QR} $$

则称之为 $\boldsymbol{A}$ 的**QR分解**或*酉-三角分解**。当 $\boldsymbol{A} \in \mathbf{R}^{n \times n}$时，称为 $\boldsymbol{A}$ 的**正交-三角分解**。

**定理** &nbsp; 任意 $\boldsymbol{A} \in \mathbf{C}^{n \times n}$都可以作QR分解，有两种分解方法：

+ $ \boldsymbol{A} = \boldsymbol{H}\_1 \boldsymbol{H}\_2 \cdots \boldsymbol{H}\_{n-1} \mathbf{R} = \boldsymbol{QR} $
+ $ \boldsymbol{A} = \boldsymbol{T}\_{12}^H \cdots \boldsymbol{T}\_{1n}^H \boldsymbol{T}\_{23}^H \cdots \boldsymbol{T}\_{2n}^H \cdots \boldsymbol{T}\_{n-1,n}^H \mathbf{R} = \boldsymbol{QR} $

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{n \times n}_n$，则 $\boldsymbol{A}$ 可唯一地分解为

$$ \boldsymbol{A} = \boldsymbol{QR} $$

其中$\boldsymbol{Q}$是$n$阶酉矩阵，$\mathbf{R} \in \mathbf{C}^{n \times n}_n$是具有正对焦元的上三角矩阵。

**上面这个定理还可以推广到长方阵上**

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}_n$，则 $\boldsymbol{A}$ 可唯一地分解为

$$ \boldsymbol{A} = \boldsymbol{QR} $$

其中$\boldsymbol{Q} \in \mathbf{C}^{m \times n}_n$且满足$\boldsymbol{Q}^H\boldsymbol{Q} = \boldsymbol{I}$，$\mathbf{R} \in \mathbf{C}^{n \times n}_n$是具有正对焦元的上三角矩阵。

## Matlab命令

    qr

# 满秩分解

**定义** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}\_r(r \gt 0)$。如果存在$\boldsymbol{F} \in \mathbf{C}^{m \times r}\_r$和$\boldsymbol{G} \in \mathbf{C}^{r \times n}\_r$，
使得

$$ \boldsymbol{A} = \boldsymbol{FG} $$

则称之为 $\boldsymbol{A}$ 的**满秩分解**。

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}\_r(r \gt 0)$，则 $boldsymbol{A}$ 的满秩分解总存在。

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}\_r(r \gt 0)$，且 $\boldsymbol{A}$ 的Hermite标准型为$\boldsymbol{H}$。取 $\boldsymbol{A}$ 的第$$j_1,j_2,\cdots,j_r$$列构成矩阵
$\boldsymbol{F}$，又取$\boldsymbol{H}$的前$r$行构成矩阵$\boldsymbol{G}$，则$\boldsymbol{A} = \boldsymbol{FG}$即为$\boldsymbol{A}$的一个满秩分解。

## Matlab程序

    TODO: 满秩分解的Matlab程序

# 奇异值分解SVD

## 酉相似与奇异值

**定义** &nbsp; 设 $\boldsymbol{A}, \boldsymbol{B} \in \mathbf{C}^{m \times n}$。若存在$m$阶酉矩阵 $\boldsymbol{U}$ 和$n$阶酉矩阵 $\boldsymbol{V}$，使得$\boldsymbol{U}^H\boldsymbol{A}\boldsymbol{V} = \boldsymbol{B}$
则称$\boldsymbol{A}$与$\boldsymbol{B}$**酉等价**。

**定义** &nbsp; 设 $$\boldsymbol{A} \in \mathbf{C}^{m \times n}_r(r \gt 0)$$，$\boldsymbol{A}^H\boldsymbol{A}$的特征值为

$$ \lambda_1 \geq \lambda_2 \geq \cdots \geq \lambda_r \ge \lambda_{r+1} = \cdots = \lambda_n = 0 $$

则称$$\sigma_i = \sqrt{\lambda_i}(i=1,2,\cdots,n)$$为$\boldsymbol{A}$的**奇异值**。

**定理** &nbsp; 酉相似矩阵具有相同奇异值

## 奇异值分解

**定义** &nbsp; 设$\boldsymbol{A} \in \mathbf{C}^{m \times n}_r(r \gt 0)$，则存在$m$阶酉矩阵$\boldsymbol{U}$和$n$阶酉矩阵$\boldsymbol{v}$，使得

$$ \boldsymbol{U}^H\boldsymbol{A}\boldsymbol{V} = \begin{pmatrix} \boldsymbol{\Sigma} & \boldsymbol{O} \\\ \boldsymbol{O} & \boldsymbol{O} \end{pmatrix} $$

其中 $$\Sigma = diag(\sigma_1,\sigma_2,\cdots,\sigma_r)$$，而$$\sigma_i(i=1,2,\cdots,r)$$为$\boldsymbol{A}$的非零奇异值。将上式改写为

$$ \boldsymbol{A} = \boldsymbol{U} \begin{pmatrix} \boldsymbol{\Sigma} & \boldsymbol{O} \\\ \boldsymbol{O} & \boldsymbol{O} \end{pmatrix} \boldsymbol{V}^H $$

称之为 $\boldsymbol{A}$ 的**奇异值分解**。

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{n \times n}$，则 $\boldsymbol{A}$ 可分解为

$$ \boldsymbol{A} = \boldsymbol{BQ} = \boldsymbol{QC} $$

其中 $\boldsymbol{Q}$ 是$n$阶酉矩阵，$\boldsymbol{B}$和$\mathbf{C}$是Hermite半正定矩阵。称上式为矩阵 $\boldsymbol{A}$ 的**极分解**。

## SVD重要应用

SVD有两个重要应用：

+ 求极小范数最小二乘解（或Moore—Penrose逆 $\boldsymbol{A}^+$）
+ 数据降维/压缩，如经典的**PCA**

### 求极小范数最小二乘解

**定理** &nbsp; 设 $\boldsymbol{A} \in \mathbf{C}^{m \times n}\_r，\boldsymbol{b} \in \mathbf{C}^{m}$，且 $\boldsymbol{A}$ 的SVD为

$$ \boldsymbol{A} = \boldsymbol{U} \begin{pmatrix} \boldsymbol{\Sigma} & \boldsymbol{O} \\\ \boldsymbol{O} & \boldsymbol{O} \end{pmatrix} \boldsymbol{V}^H $$

则

$$ \boldsymbol{x}^{(0)} = \boldsymbol{V} \begin{pmatrix} \boldsymbol{\Sigma}^{-1} & \boldsymbol{O} \\\ \boldsymbol{O} & \boldsymbol{O} \end{pmatrix} \boldsymbol{U}^H \boldsymbol{b} $$

是矛盾方程组 $\boldsymbol{A}\boldsymbol{x} = \boldsymbol{b}$ 的最小二乘解；如果该方程组的最小二乘解不唯一，则 $\boldsymbol{x}^{(0)}$ 是其中具有最小2范数的向量，
称之为 $\boldsymbol{A}\boldsymbol{x} = \boldsymbol{b}$ 的**极小范数最小二乘解**，而矩阵

$$ \boldsymbol{A}^{+} = \boldsymbol{V} \begin{pmatrix} \boldsymbol{\Sigma}^{-1} & \boldsymbol{O} \\\ \boldsymbol{O} & \boldsymbol{O} \end{pmatrix} \boldsymbol{U}^H $$

称为矩阵 $\boldsymbol{A}$ 的**Moore-Penrose逆**。

### 数据压缩 —— PCA

这方面的文章非常多，推荐Standford [CS229)](http://cs229.stanford.edu) Andrew Ng的讲义。

这里补充一点，就是如何通过SVD求协方差矩阵的特征值和特征向量。

设数据矩阵为 $\boldsymbol{X} \in \mathbf{C}^{m \times n}$（其每列已减去均值，即alread zero-mean），根据协方差的定义，我们有协方差矩阵

$$ cov(\boldsymbol{X}) = \frac{1}{m-1} \boldsymbol{X}^H \boldsymbol{X} $$

显然，协方差矩阵的特征值和特征向量即为 $\boldsymbol{X}^H \boldsymbol{X}$ 的特征值和特征向量差个常数因子$\frac{1}{m-1}$。而 $\boldsymbol{X}^H \boldsymbol{X}$ 的特征值和特征向量可由对 $\boldsymbol{X}$ 进行SVD求得：

+ 特征值为 $\boldsymbol{D}^2$
+ 特征向量为 $\boldsymbol{V}$

因此我们就通过SVD直接求出了协方差矩阵的特征值和特征向量，而避免了计算协方差矩阵的开销。

## Matlab命令

    svd
