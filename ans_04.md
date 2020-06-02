# 课后作业4

#### 1. 给出下列数据, 用最小二乘法求形如$y = ae^{bx}$的经验公式. (5分)
|       |       |       |      |      |
|:-----:|:-----:|:-----:|:----:|:----:|
| $x_i$ | -0.60 | -0.50 | 0.25 | 0.75 |
| $y_i$ | 1.00  | 1.25  | 2.50 | 4.25 |
解: 对$y = ae^{bx}$两端同时作用对数函数得到, $\ln{y} = \ln{a} + bx$  
令$z_i = \ln{y_i}$, 可得离散数据$\{(x_i, z_i)\}_{i=1}^4$

|       |       |       |      |      |
|:-----:|:-----:|:-----:|:----:|:----:|
| $x_i$ | -0.60 | -0.50 | 0.25 | 0.75 |
| $z_i$ | 0.0  | 0.2231  | 0.9163 | 1.4469 |

对数组$\{(x_i, z_i)\}_{i=1}^4$进行线性拟合$z = A + Bx$, 可得**法方程**为 (课本50页, 2.1式)
$$
\begin{pmatrix}
    4 & \sum\limits_{i=1}^4 x_i \\
    \sum\limits_{i=1}^4 x_i & \sum\limits_{i=1}^4 x_i^2
\end{pmatrix}
\begin{pmatrix}
    A \\
    B
\end{pmatrix}
=
\begin{pmatrix}
    \sum\limits_{i=1}^4 z_i \\
    \sum\limits_{i=1}^4 x_i z_i
\end{pmatrix}
\Rightarrow
\begin{pmatrix}
    4 & -0.1 \\
    -0.1 & 1.235
\end{pmatrix}
\begin{pmatrix}
    A \\
    B
\end{pmatrix}
=
\begin{pmatrix}
    2.5863 \\
    1.2027
\end{pmatrix}
$$
$$
\Rightarrow
\begin{pmatrix}
    A \\
    B
\end{pmatrix}
=
\begin{pmatrix}
    0.6723 \\
    1.0283
\end{pmatrix}
$$
得到 $a = e^A = 1.9587, \quad b = B = 1.0283$

即 $y = 1.9587e^{1.0283x}$

---

#### 2. 在最小二乘法原理下求下列矛盾方程组: (5分)
$$
\left\{
\begin{gathered}
    x_1 - 2x_2 = 4 \\
    x_1 + 6x_2 = 14 \\
    3x_1 + x_2 = 7.5 \\
    x_1 + x_2 = 4.5
\end{gathered}
\right.
$$
解: 将线性方程组写成矩阵的形式 $Ax = Y$
$$
\begin{pmatrix}
    1 & -2 \\
    1 & 6 \\
    3 & 1 \\
    1 & 1
\end{pmatrix}
\begin{pmatrix}
    x_1 \\
    x_2
\end{pmatrix}
=
\begin{pmatrix}
    4 \\
    14 \\
    7.5 \\
    4.5
\end{pmatrix}
$$
矛盾方程组$Ax = Y$的法方程为$A^T Ax = A^T Y$ (课本55-56页)
$$
\begin{pmatrix}
    1 & 1 & 3 & 1 \\
    -2 & 6 & 1 & 1
\end{pmatrix}
\begin{pmatrix}
    1 & -2 \\
    1 & 6 \\
    3 & 1 \\
    1 & 1
\end{pmatrix}
\begin{pmatrix}
    x_1 \\
    x_2
\end{pmatrix}
=
\begin{pmatrix}
    1 & 1 & 3 & 1 \\
    -2 & 6 & 1 & 1
\end{pmatrix}
\begin{pmatrix}
    4 \\
    14 \\
    7.5 \\
    4.5
\end{pmatrix}
$$
$$
\Rightarrow
\begin{pmatrix}
    12 & 8 \\
    8 & 42
\end{pmatrix}
\begin{pmatrix}
    x_1 \\
    x_2
\end{pmatrix}
=
\begin{pmatrix}
    45 \\
    88
\end{pmatrix}
$$
解得
$$
\begin{pmatrix}
    x_1 \\
    x_2
\end{pmatrix}
=
\begin{pmatrix}
    \frac{593}{220} \\
    \frac{87}{55}
\end{pmatrix}
=
\begin{pmatrix}
    2.69545 \\
    1.58182
\end{pmatrix}
$$

---

#### 3. 利用最小二乘法构造二次多项式$y = p(x)$去拟合下列数据(这里$x$代表年份, $y$为人数), 并计算$y(2015)$, 结果精确到小数点后一位. (8分)
|     |        |        |        |        |        |
|:---:|:------:|:------:|:------:|:------:|:------:|
| $x$ | 2010   | 2011   | 2012   | 2013   | 2014   |
| $y$ | 134091 | 134735 | 135404 | 136072 | 136782 |
解: 设$p(x) = a(x -2012)^2 + b(x - 2012) + c + 135404$, 得到矛盾方程组
$$
\quad\;\begin{pmatrix}
    4 & -2 & 1 \\
    1 & -1 & 1 \\
    0 & 0 & 1 \\
    1 & 1 & 1 \\
    4 & 2 & 1
\end{pmatrix}
\begin{pmatrix}
    a \\
    b \\
    c
\end{pmatrix}
=
\begin{pmatrix}
    -1313 \\
    -669 \\
    0 \\
    668 \\
    1378
\end{pmatrix}
$$
$$
\Rightarrow
\begin{pmatrix}
    34 & 0 & 10 \\
    0 & 10 & 0 \\
    10 & 0 & 5
\end{pmatrix}
\begin{pmatrix}
    a \\
    b \\
    c
\end{pmatrix}
=
\begin{pmatrix}
    259 \\
    6719 \\
    64
\end{pmatrix}
$$
解得
$$
\left\{
\begin{aligned}
    a &= \frac{131}{14} \\
    b &= \frac{6719}{10} \\
    c &= -\frac{207}{35}
\end{aligned}
\right.
\qquad p(2015) = 9a + 3b +c +135404 = 137498.0
$$
