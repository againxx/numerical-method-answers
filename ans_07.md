# 课后作业7

#### 1. 设有线性代数方程组$Ax=b$, 其中,

$$
A=
\begin{pmatrix}
    \begin{array}{rrrr}
        2 & -1 & 0 & 0 \\
        -1 & 2 & -1 & 0 \\
        0 & -1 & 2 & -1 \\
        0 & 0 & -1 & 2
    \end{array}
\end{pmatrix},\quad
b=
\begin{pmatrix}
    2 \\
    0 \\
    2 \\
    1
\end{pmatrix}
$$

(a) 求Jacobi迭代的迭代矩阵及相应的迭代格式; (4分)

(b) 讨论此时Jacobi迭代（方法）的收敛性. (6分)

解: (a) Jacobi迭代矩阵 (课本99页)
$$
\begin{aligned}
    R &= I - D^{-1}A \\
      &= I -
    \begin{pmatrix}
        2 & & & \\
        & 2 & & \\
        & & 2 & \\
        & & & 2
    \end{pmatrix}^{-1}
    \begin{pmatrix}
        \begin{array}{rrrr}
            2 & -1 & 0 & 0 \\
            -1 & 2 & -1 & 0 \\
            0 & -1 & 2 & -1 \\
            0 & 0 & -1 & 2
        \end{array}
    \end{pmatrix} \\
      &= I -
    \begin{pmatrix}
        \frac{1}{2} & & & \\
        & \frac{1}{2} & & \\
        & & \frac{1}{2} & \\
        & & & \frac{1}{2}
    \end{pmatrix}
    \begin{pmatrix}
        \begin{array}{rrrr}
            2 & -1 & 0 & 0 \\
            -1 & 2 & -1 & 0 \\
            0 & -1 & 2 & -1 \\
            0 & 0 & -1 & 2
        \end{array}
    \end{pmatrix} \\
      &= I -
    \begin{pmatrix}
        \begin{array}{rrrr}
            1 & -\frac{1}{2} & 0 & 0 \\
            -\frac{1}{2} & 1 & -\frac{1}{2} & 0 \\
            0 & -\frac{1}{2} & 1 & -\frac{1}{2} \\
            0 & 0 & -\frac{1}{2} & 1
        \end{array}
    \end{pmatrix} \\
      &=
    \begin{pmatrix}
        \begin{array}{rrrr}
            0 & \frac{1}{2} & 0 & 0 \\
            \frac{1}{2} & 0 & \frac{1}{2} & 0 \\
            0 & \frac{1}{2} & 0 & \frac{1}{2} \\
            0 & 0 & \frac{1}{2} & 0
        \end{array}
    \end{pmatrix} \\
\end{aligned}
$$

迭代常数项向量 $g = D^{-1}b = (1, 0, 1, \frac{1}{2})^T$

迭代格式的矩阵形式 $X^{(k+1)} = R X^{(k)} + g$

分量形式:

$$
\left\{
\begin{aligned}
    x_1^{(k+1)} &= \frac{1}{2} x_2^{(k)} + 1 \\
    x_2^{(k+1)} &= \frac{1}{2} x_1^{(k)} + \frac{1}{2} x_3^{(k)} \\
    x_3^{(k+1)} &= \frac{1}{2} x_2^{(k)} + \frac{1}{2} x_4^{(k)} + 1 \\
    x_4^{(k+1)} &= \frac{1}{2} x_3^{(k)} + \frac{1}{2} \\
\end{aligned}
\right.
$$

(b) 注意, A不是~~严格~~对角优, 不能以此作为收敛性的判断条件.
迭代收敛的 **充分必要** 条件是迭代矩阵的谱半径$\rho(R) = \max\limits_{1\leq i \leq n}|\lambda_i| < 1$

$$
\begin{aligned}
    \det(\lambda I - R) &=
    \begin{vmatrix}
        \lambda & -\frac{1}{2} & & \\
        -\frac{1}{2} & \lambda & -\frac{1}{2} & \\
        & -\frac{1}{2} & \lambda & -\frac{1}{2} \\
        & & -\frac{1}{2} & \lambda
    \end{vmatrix} \\
    &= \lambda
    \begin{vmatrix}
        \lambda & -\frac{1}{2} & \\
        -\frac{1}{2} & \lambda & -\frac{1}{2} \\
        & -\frac{1}{2} & \lambda
    \end{vmatrix}
    + \frac{1}{2}
    \begin{vmatrix}
        -\frac{1}{2} & -\frac{1}{2} & \\
        & \lambda & -\frac{1}{2} \\
        & -\frac{1}{2} & \lambda
    \end{vmatrix} \\
    &= \lambda(\lambda^3 - \frac{1}{2} \lambda) + \frac{1}{2}(-\frac{1}{2}(\lambda^2 - \frac{1}{4})) \\
    &= \lambda^4 - \frac{3}{4} \lambda^2 + \frac{1}{16}
\end{aligned}
$$

$$
\Rightarrow \lambda^2 = \frac{3 \pm \sqrt{5}}{8}
$$
$$
\Rightarrow |\lambda_1| = |\lambda_2| = \sqrt{\frac{3 + \sqrt{5}}{8}} = 0.809017, \ 
|\lambda_3| = |\lambda_4| = \sqrt{\frac{3 - \sqrt{5}}{8}} = 0.309017
$$

故而, $\rho(R) = \max\limits_{1\leq i \leq 4}|\lambda_i| = 0.809017 < 1$, Jacobi迭代收敛.

---

#### 2. 设有线性代数方程组

$$
\left\{
\begin{aligned}
    5x_1 - 3x_2 + 2x_3 &= 5 \\
    -3x_1 + 5x_2 + 2x_3 &= 5 \\
    2x_1 + 2x_2 + 5x_3 &= 5
\end{aligned}
\right.
$$

(a) 分别写出Gauss-Seidel迭代和SOR迭代的分量形式; (4分)

(b) 求Gauss-Seidel迭代的分裂矩阵(splitting matrix) (2分) 及迭代矩阵(iteration matrix); (6分)

\(c\) 讨论Gauss-Seidel迭代的收敛性(请给出理由或证明). (6分)

解: (a) 原方程组可写为
$$
\left\{
\begin{aligned}
    x_1 &= \frac{1}{5}(3x_2 - 2x_3 + 5) \\
    x_2 &= \frac{1}{5}(3x_1 - 2x_3 + 5) \\
    x_3 &= \frac{1}{5}(-2x_1 - 2x_2 + 5)
\end{aligned}
\right.
$$

$\implies \,$Gauss-Seidel迭代的分量形式 (课本102页, 5.6式)

$$
\left\{
\begin{aligned}
    x_1^{(k+1)} &= \frac{1}{5}(3x_2^{(k)} - 2x_3^{(k)} + 5) \\
    x_2^{(k+1)} &= \frac{1}{5}(3x_1^{(k+1)} - 2x_3^{(k)} + 5) \\
    x_3^{(k+1)} &= \frac{1}{5}(-2x_1^{(k+1)} - 2x_2^{(k+1)} + 5)
\end{aligned}
\right.
$$

$\implies \,$SOR迭代的分量形式 (课本105页, 5.10式)

$$
\left\{
\begin{aligned}
    x_1^{(k+1)} &= (1 - \omega) x_1^{(k)} + \frac{\omega}{5}(3x_2^{(k)} - 2x_3^{(k)} + 5) \\
    x_2^{(k+1)} &= (1 - \omega) x_2^{(k)} + \frac{\omega}{5}(3x_1^{(k+1)} - 2x_3^{(k)} + 5) \\
    x_3^{(k+1)} &= (1 - \omega) x_3^{(k)} + \frac{\omega}{5}(-2x_1^{(k+1)} - 2x_2^{(k+1)} + 5)
\end{aligned}
\right.
$$
(b) Gauss-Seidel的分裂矩阵为 (PPT ch5, 23页)

$$
Q = D + L =
\begin{pmatrix}
    5 & 0 & 0 \\
    -3 & 5 & 0 \\
    2 & 2 & 5
\end{pmatrix}
$$

Gauss-Seidel的迭代矩阵为
$$
\begin{aligned}
    G &= I - Q^{-1}A = -(D+L)^{-1}U = -Q^{-1}U \\
    &= -
    \begin{pmatrix}
        5 & 0 & 0 \\
        -3 & 5 & 0 \\
        2 & 2 & 5
    \end{pmatrix}^{-1}
    \begin{pmatrix}
        0 & -3 & 2 \\
        0 & 0 & 2 \\
        0 & 0 & 0
    \end{pmatrix}
    =
    \begin{pmatrix}
        0 & \frac{3}{5} & -\frac{2}{5} \\
        0 & \frac{9}{25} & -\frac{16}{25} \\
        0 & -\frac{48}{125} & \frac{52}{125}
    \end{pmatrix}
\end{aligned}
$$

\(c\) 法一: 根据书上定理5.4, 当A对称正定时, Gauss-Seidel迭代收敛.
而实对称正定的等价条件之一便是所有顺序主子式大于0, 下面即验证A的所有顺序主子式大于零.

$$
D_1 =
\begin{vmatrix}
    5
\end{vmatrix} = 5 > 0
$$
$$
D_2 =
\begin{vmatrix}
    5 & -3 \\
    -3 & 5
\end{vmatrix} = 16 > 0
$$
$$
D_3 =
\begin{vmatrix}
    5 & -3 & 2 \\
    -3 & 5 & 2 \\
    2 & 2 & 5
\end{vmatrix} = 16 \times 5 - 2 \times
\begin{vmatrix}
    5 & 2 \\
    -3 & 2
\end{vmatrix} + 2 \times
\begin{vmatrix}
    -3 & 2 \\
    5 & 2
\end{vmatrix} = 16 > 0
$$

故A对称正定, Gauss-Seidel迭代收敛

法二: 计算迭代矩阵$G$的谱半径

$$
\begin{aligned}
    \det(\lambda I - G) &=
    \begin{vmatrix}
        \lambda & -\frac{3}{5} & \frac{2}{5} \\
        0 & \lambda - \frac{9}{25} & \frac{16}{25} \\
        0 & \frac{48}{125} & \lambda - \frac{52}{125}
    \end{vmatrix} = \lambda
    \begin{vmatrix}
        \lambda - \frac{9}{25} & \frac{16}{25} \\
        \frac{48}{125} & \lambda - \frac{52}{125}
    \end{vmatrix} \\
    &= \lambda(\lambda^2 - \frac{97}{125} \lambda - \frac{12}{125}) = 0
\end{aligned}
$$

$$
\Rightarrow \ \lambda_1 = 0, \lambda_2 = \frac{97 + \sqrt{15409}}{250}, \lambda_3 = \frac{97 - \sqrt{15409}}{250}
$$

$$
\rho(G) = \frac{97 + \sqrt{15409}}{250} = 0.884532 < 1
$$

故Gauss-Seidel迭代收敛

另可以, 将$\lambda = -1, \lambda = 0, \lambda = 1$代入$f(\lambda) = \lambda^2 - \frac{97}{125} \lambda - \frac{12}{125}$中验证

得到$f(-1) > 0, f(0) < 0, f(1) > 0$得到$f(\lambda)$在$(-1, 1)$间必有两个零点, 所以$|\lambda_2| < 1, |\lambda_3| < 1$
