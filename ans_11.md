# 课后作业11

#### 1. 试推导如下Runge-Kutta公式的局部截断误差和精度 (提示: 利用二元函数的Taylor展开). (10分)
$$
\left\{
\begin{aligned}
    y_{n+1} &= y_n + \frac{h}{4}(3k_1 + k_2) \\
         k_1 &= f(x_n, y_n) \\
         k_2 &= f(x_n + 2h, y_n + 2hk_1)
\end{aligned}
\right.
$$

解: 思路还是将公式右端在$x_n$处作Taylor展开, 重点是如何将$k_2$展开成$y(x_n)$各阶导数的形式

下面先对$k_2$在$(x_n, y_n)$处作二元Taylor展开
$$
\begin{aligned}
    k_2 &= f(x_n + 2h, y_n + 2hk_1) \\
        &= f(x_n, y_n) + 2hf_x(x_n, y_n) + 2hk_1 f_y(x_n, y_n) + 2h^2 f_{xx}(x_n, y_n) \\
        &+ 4h^2 k_1 f_{xy}(x_n, y_n) + 2h^2 k_1^2 f_{yy}(x_n, y_n) + O(h^3)
\end{aligned}
$$

接下来利用$y''$和$y^{(3)}$消去部分$f$的偏导项
$$
y''(x) = \frac{d}{dx} \frac{dy}{dx} = \frac{d}{dx} f(x, y) = f_x + f_y y' = f_x + f_y f
$$
$$
\begin{aligned}
    y^{(3)}(x) &= \frac{d}{dx} (f_x + f_y f) = f_{xx} + f_{xy}y' + \frac{d}{dx}(f_y f) \\
               &= f_{xx} + f_{xy} y' + \frac{d}{dx}(f_y)f + f_y \frac{d}{dx}(f) \\
               &= f_{xx} + f_{xy}y' + f_{yx}y' + f_{yy}(y')^2 + f_y f_x + (f_y)^2 y' \\
               &= f_{xx} + 2f_{xy}y' + f_{yy}(y')^2 + f_y y''
\end{aligned}
$$

将$x = x_n, y = y_n$代入并移项, 可得
$$
\begin{aligned}
    &f_x(x_n, y_n) + k_1 f_y(x_n, y_n) = y''(x_n) \\
    &f_{xx}(x_n, y_n) + 2k_1 f_{xy}(x_n, y_n) + k_1^2 f_{yy}(x_n, y_n) = y^{(3)}(x_n) - f_y(x_n, y_n)y''(x_n)
\end{aligned}
$$

将上面两个等式代入$k_2$的展开式
$$
k_2 = y'(x_n) + (2h - 2h^2 f_y)y''(x_n) + 2h^2 y^{(3)}(x_n) + O(h^3)
$$

将$y(x_{n+1})$也在$x_n$点Taylor展开, 整合成下表

|                                           | $y(x_n)$ | $y'(x_n)$ |               $y''(x_n)$              |   $y^{(3)}(x_n)$  |
|:-----------------------------------------:|:--------:|:---------:|:-------------------------------------:|:-----------------:|
|                   $k_1$                   |          |    $1$    |                                       |                   |
|                   $k_2$                   |          |    $1$    |            $2h - 2h^2 f_y$            |       $2h^2$      |
| $y_{n+1} = y_n + \frac{h}{4}[3k_1 + k_2]$ |    $1$   |    $h$    | $\frac{1}{2}h^2 - \frac{1}{2}h^3 f_y$ |  $\frac{1}{2}h^3$ |
|                $y(x_{n+1})$               |    $1$   |    $h$    |            $\frac{1}{2}h^2$           |  $\frac{1}{6}h^3$ |
|           $y(x_{n+1}) - y_{n+1}$          |          |           |          $\frac{1}{2}h^3 f_y$         | $-\frac{1}{3}h^3$ |

可以看出该Runge-Kutta公式的局部截断误差为$O(h^3)$, 精度为2阶

---

#### 2. 讨论梯形格式$y_{n+1} = y_n + \frac{h}{2}[f(x_n, y_n) + f(x_{n+1}, y_{n+1})]$的绝对稳定性($h>0$). (10分)
解: 误差方程为
$$
\rho_{n+1} = \rho_n + \frac{\lambda h}{2}(\rho_n + \rho_{n+1})
\implies (1 - \frac{\lambda h}{2})\rho_{n+1} = (1 + \frac{\lambda h}{2}) \rho_n
$$

计算相邻两步误差的比值
$$
\left| \frac{\rho_{n+1}}{\rho_n} \right| = \left| \frac{2 + \lambda h}{2 - \lambda h} \right|
$$

由于 $Re(\lambda) < 0$, 对任意$h$, 恒有$\left| \frac{\rho_{n+1}}{\rho_n} \right| = \left| \frac{2 + \lambda h}{2 - \lambda h} \right| < 1$

因此梯形格式的稳定区域是整个左半复平面, 为无条件绝对稳定.

---

#### 3. 用幂法估算下面矩阵的按模最大的特征值和相应的特征向量(取初始向量$(1,1)^T$, 迭代5次即可). (6分)
$$
A =
\begin{pmatrix}
    2 & 2 \\
    1 & 4
\end{pmatrix}
$$

解:
$$
X^{(0)} = \left( \begin{matrix} 1 \\ 1 \end{matrix}\right),
X^{(1)} = A \cdot X^{(0)} = \left(\begin{matrix} 4 \\ 5 \end{matrix}\right),
X^{(2)} = A \cdot X^{(1)} = \left(\begin{matrix} 18 \\ 24 \end{matrix}\right),
$$
$$
X^{(3)} = A \cdot X^{(2)} = \left(\begin{matrix} 84 \\ 114 \end{matrix}\right),
X^{(4)} = A \cdot X^{(3)} = \left(\begin{matrix} 396 \\ 540 \end{matrix}\right),
$$
$$
X^{(5)} = A \cdot X^{(4)} = \left(\begin{matrix} 1872 \\ 2556 \end{matrix}\right),
$$

观察前后两个向量对应分量的比值
$$
\begin{aligned}
    \frac{x_1^{(5)}}{x_1^{(4)}} &= \frac{1872}{396} = 4.727273,
    &\frac{x_2^{(5)}}{x_2^{(4)}} = \frac{2556}{540} = 4.733333  \\
    \frac{x_1^{(4)}}{x_1^{(3)}} &= \frac{396}{84} = 4.714286,
    &\frac{x_2^{(4)}}{x_2^{(3)}} = \frac{540}{114} = 4.736842 \\
\end{aligned}
$$

可以看到比值趋于一个稳定的值, 即按模最大的特征值一个,

得到特征值 $\lambda_1 \approx 4.7273$, 特征向量$X^{(5)} = (1872, 2556)^T$

---

#### 4. 考虑用Jacobi方法计算矩阵A的全部特征值. 求对A作第一次Givens相似变换时的Givens变换矩阵(要求相应的计算效率最高). (6分)
$$
A =
\begin{pmatrix}
    3 & 1 & 2 \\
    1 & 5 & 0 \\
    2 & 0 & 7
\end{pmatrix}
$$

解: 为了计算效率最高, 可以选取$p=1, q=3$, 构造Givens变换矩阵形式如下
$$
Q(1, 3, \theta) =
\begin{pmatrix}
    \cos\theta & 0 & \sin\theta \\
    0 & 1 & 0 \\
    -\sin\theta & 0 & \cos\theta
\end{pmatrix}
$$

做一次变换后, $B = Q^T A Q$, 可得到
$$
b_{13} = b_{31} = 2\cos2\theta + \frac{3 - 7}{2}\sin2\theta = 2\cos 2\theta - 2\sin 2\theta
$$

令$b_{13} = b_{31} = 0$, 可得$t^2 + 2t - 1 = 0$, 其中$t = \tan \theta$

求得$t = -1 + \sqrt{2}$ (绝对值较小的根)

$$
\left\{
\begin{aligned}
    \cos \theta &= \frac{1}{\sqrt{1 + t^2}} = \frac{1}{\sqrt{4-2\sqrt{2}}} = 0.92388 \\
    \sin \theta &= \frac{t}{\sqrt{1 + t^2}} = \frac{\sqrt{2} - 1}{\sqrt{4-2\sqrt{2}}} = 0.38268
\end{aligned}
\right.
$$

最后得到Givens变换矩阵如下:
$$
Q(1, 3) =
\begin{pmatrix}
    0.92388 & 0 & 0.38268 \\
    0 & 1 & 0 \\
    -0.38268 & 0 & 0.92388
\end{pmatrix}
$$
