# 课后作业11

#### 1. 试推导如下Runge-Kutta公式的局部截断误差和精度 (提示: 利用二元函数的Taylor展开). (12分)
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

#### 2. 讨论梯形格式$y_{n+1} = y_n + \frac{h}{2}[f(x_n, y_n) + f(x_{n+1}, y_{n+1})]$的绝对稳定性($h>0$). (8分)
