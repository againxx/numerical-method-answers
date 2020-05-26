# 课后作业6

#### 1. 分别计算下列矩阵的$\|\cdot\|_1$, $\|\cdot\|_\infty$范数: (4分)
$$
(a) \  A =
\begin{pmatrix}
    \begin{array}{rrr}
        5 & -2 & 1 \\
        -1 & 3 & -1 \\
        -1 & 2 & -6
    \end{array}
\end{pmatrix},
(b) \  A =
\begin{pmatrix}
    \begin{array}{rrr}
        4 & -1 & 1 \\
        -2 & 3 & 1 \\
        -1 & 1 & 6
    \end{array}
\end{pmatrix}
$$

解: 记忆方式,
* 1是竖着的所以是`列`(绝对值)和的最大值
* $\infty$是横着的所以是`行`(绝对值)和的最大值

(a) $\|A\|_1 = \max\{7, 7, 8\} = 8$

$\ \quad\|A\|_\infty = \max\{8, 5, 9\} = 9$

(b) $\|A\|_1 = \max\{7, 5, 8\} = 8$

$\ \quad\|A\|_\infty = \max\{6, 6, 8\} = 8$

---

#### 2. 分别计算矩阵$A = \bigl( \begin{smallmatrix} \ \ 4 & -2 \\ -1 & \ \ \ 1 \end{smallmatrix} \bigr)$的谱半径及其$\|\cdot\|_2$范数。(4分)
解:
$$
\det(\lambda I - A) =
\begin{vmatrix}
    \lambda - 4 & 2 \\
    1 & \lambda - 1
\end{vmatrix}

= (\lambda - 4)(\lambda - 1) - 2 = \lambda^2 - 5 \lambda + 2
$$
$$
\Rightarrow \lambda_1 = \frac{5+\sqrt{17}}{2} = 4.56155 \qquad \lambda_2 = \frac{5-\sqrt{17}}{2} = 0.43845
$$
所以$A$的谱半径, $\rho(A) = \frac{5+\sqrt{17}}{2} = 4.56155$

根据2范数的定义, $\|A\|_2 = \sqrt{\rho(A^T A)}$, 所以
$$
A^T A =
\begin{pmatrix}
    4 & -1 \\
    -2 & 1
\end{pmatrix}
\begin{pmatrix}
    4 & -2 \\
    -1 & 1
\end{pmatrix}
=
\begin{pmatrix}
    17 & -9 \\
    -9 & 5
\end{pmatrix}
$$
$$
\det(\lambda I - A^T A) =
\begin{vmatrix}
    \lambda - 17 & 9    \\
    9 & \lambda - 5
\end{vmatrix}
= \lambda^2 -22 \lambda + 4 = 0
$$
$$
\Rightarrow \lambda_1 = 11 + 3 \sqrt{13} \qquad \lambda_2 = 11 - 3 \sqrt{13}
$$
从而
$$
\|A\|_2 = \sqrt{11 + 3 \sqrt{13}} = \frac{\sqrt{26} + 3 \sqrt{2}}{2} = 4.67083
$$

---

#### 3. 用Doolittle分解法解下列线性方程组（请给出详细的解题过程，包括矩阵分解）（LU分解6分，解方程4分，共10分)
$$
\left\{
    \begin{aligned}
        5x_1 + x_2 + 2x_3 &= 10 \\
        x_1 + 3x_2 - x_3 &= 5 \\
        2x_1 + x_2 + 5x_3 &= 20
    \end{aligned}
\right.
$$
解: Doolittle分解, $A = LU$, 其中$L$为单位下三角阵, $U$为上三角阵
$$
\begin{aligned}
    \begin{pmatrix}
        5 & 1 & 2 \\
        1 & 3 & -1 \\
        2 & 1 & 5
    \end{pmatrix}
    &=
    \begin{pmatrix}
        1 & \  & \  \\
        l_{21} & 1 & \  \\
        l_{31} & l_{32} & 1
    \end{pmatrix}
    \begin{pmatrix}
        u_{11} & u_{12} & u_{13} \\
        \   & u_{22} & u_{23} \\
        \   & \   & u_{33}
    \end{pmatrix} \\
    &=
    \begin{pmatrix}
        1 & \  & \  \\
        l_{21} & 1 & \  \\
        l_{31} & l_{32} & 1
    \end{pmatrix}
    \begin{pmatrix}
        5   & 1   & 2 \\
        \   & u_{22} & u_{23} \\
        \   & \   & u_{33}
    \end{pmatrix} \\
    &=
    \begin{pmatrix}
        1 & \  & \  \\
        \frac{1}{5} & 1 & \  \\
        \frac{2}{5} & l_{32} & 1
    \end{pmatrix}
    \begin{pmatrix}
        5   & 1   & 2 \\
        \   & \frac{14}{5} & -\frac{7}{5} \\
        \   & \   & u_{33}
    \end{pmatrix} \\
    &=
    \underbrace{\begin{pmatrix}
        1 & \  & \  \\
        \frac{1}{5} & 1 & \  \\
        \frac{2}{5} & \frac{3}{14} & 1
    \end{pmatrix}}_L
    \underbrace{\begin{pmatrix}
        5   & 1   & 2 \\
        \   & \frac{14}{5} & -\frac{7}{5} \\
        \   & \   & \frac{9}{2}
    \end{pmatrix}}_U
\end{aligned}
$$
下面利用分解结果解线性方程组, 首先求$y$使得$Ly=b$
$$
\begin{pmatrix}
    1 & \  & \  \\
    \frac{1}{5} & 1 & \  \\
    \frac{2}{5} & \frac{3}{14} & 1
\end{pmatrix}
\begin{pmatrix}
    y_1 \\
    y_2 \\
    y_3
\end{pmatrix}=
\begin{pmatrix}
    10 \\
    5 \\
    20
\end{pmatrix}
\Rightarrow
\begin{pmatrix}
    y_1 \\
    y_2 \\
    y_3
\end{pmatrix}=
\begin{pmatrix}
    10 \\
    3 \\
    \frac{215}{14}
\end{pmatrix}=
\begin{pmatrix}
    10 \\
    3 \\
    15.3571
\end{pmatrix}
$$
再求$x$使得$Ux=y$
$$
\begin{pmatrix}
    5   & 1   & 2 \\
    \   & \frac{14}{5} & -\frac{7}{5} \\
    \   & \   & \frac{9}{2}
\end{pmatrix}
\begin{pmatrix}
    x_1 \\
    x_2 \\
    x_3
\end{pmatrix}=
\begin{pmatrix}
    10 \\
    3 \\
    \frac{215}{14}
\end{pmatrix}
\Rightarrow
\begin{pmatrix}
    x_1 \\
    x_2 \\
    x_3
\end{pmatrix}=
\begin{pmatrix}
    \frac{5}{63} \\
    \frac{25}{9} \\
    \frac{215}{63}
\end{pmatrix}=
\begin{pmatrix}
    0.0794 \\
    2.7778 \\
    3.4127
\end{pmatrix}
$$
