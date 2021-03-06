# 课后作业9

#### 1. 给定函数$f(x)$的离散值表, 分别用向前、向后及中心差商公式计算$f'(0.02), f'(0.04)$. (6分)
|        |     |      |      |      |
|:------:|:---:|:----:|:----:|:----:|
|   $x$  | 0.0 | 0.02 | 0.04 | 0.06 |
| $f(x)$ | 6.0 |  4.0 |  2.0 |  8.0 |

解: 向前、向后及中心差商的公式分别定义如下,
$$
\left\{
\begin{aligned}
    f'(x_0) &= \frac{f(x_0 + h) - f(x_0)}{h} & \small{\text{向前差商}} \\
    f'(x_0) &= \frac{f(x_0) - f(x_0 - h)}{h} & \small{\text{向后差商}} \\
    f'(x_0) &= \frac{f(x_0 + h) - f(x_0 - h)}{2h} \qquad & \small{\text{中心差商}}
\end{aligned}
\right.
$$

故, 由以上定义可知

|            | 向前差商                                   | 向后差商                                   | 中心差商                                  |
|------------|--------------------------------------------|--------------------------------------------|-------------------------------------------|
| $f'(0.02)$ | $\frac{f(0.04)-f(0.02)}{0.04-0.02}=-100.0$ | $\frac{f(0.02)-f(0.0)}{0.02-0.0}=-100.0$   | $\frac{f(0.04)-f(0.0)}{0.04-0.0}=-100.0$  |
| $f'(0.04)$ | $\frac{f(0.06)-f(0.04)}{0.06-0.04}=300.0$  | $\frac{f(0.04)-f(0.02)}{0.04-0.02}=-100.0$ | $\frac{f(0.06)-f(0.02)}{0.06-0.02}=100.0$ |

---

#### 2. 试分别推导如下差分格式(三点公式)的误差: (8分)
$$
\begin{aligned}
    f'(x_0) &\approx L_2'(x_0) = \frac{1}{2h} (-3f(x_0) + 4f(x_1) - f(x_2)) \\
    f'(x_2) &\approx L_2'(x_2) = \frac{1}{2h} (f(x_0) - 4f(x_1) + 3f(x_2))
\end{aligned}
$$
其中:
$$
\begin{aligned}
    L_2(x) &= \frac{(x-x_1)(x-x_2)}{2h^2} f(x_0) + \frac{(x-x_0)(x-x_2)}{-h^2} f(x_1) + \frac{(x-x_0)(x-x_1)}{2h^2} f(x_2) \\
    L_2'(x) &= \frac{(x-x_1+x-x_2)}{2h^2} f(x_0) + \frac{(x-x_0+x-x_2)}{-h^2} f(x_1) + \frac{(x-x_0+x-x_1)}{2h^2} f(x_2) \\
    x_2 - x_1 &= x_1 - x_0 = h
\end{aligned}
$$

解:
将$f(x_1)$, $f(x_2)$在$x_0$处做Taylor展开
$$
\begin{aligned}
    f(x_1) &= f(x_0) + hf'(x_0) + \frac{h^2}{2} f''(x_0) + \frac{h^3}{6} f^{(3)}(x_0) + O(h^4) \\
    f(x_2) &= f(x_0) + 2hf'(x_0) + 2h^2 f''(x_0) + \frac{4h^3}{3} f^{(3)}(x_0) + O(h^4)
\end{aligned}
$$

$$\implies$$
$$
\begin{aligned}
    f'(x_0) - L_2'(x_0) &= f'(x_0) -\frac{1}{2h} \lbrack 2h f'(x_0) - \frac{2}{3} h^3f^{(3)}(x_0) + O(h^4) \rbrack \\
    &= \frac{1}{3} h^2 f^{(3)}(x_0) + O(h^3)
\end{aligned}
$$

将$f(x_0)$, $f(x_1)$在$x_2$处做Taylor展开
$$
\begin{aligned}
    f(x_0) &= f(x_2) -2hf'(x_2) + 2h^2 f''(x_2) -\frac{4h^3}{3} f^{(3)}(x_2) + O(h^4) \\
    f(x_1) &= f(x_2) - hf'(x_2) + \frac{h^2}{2} f''(x_2) - \frac{h^3}{6} f^{(3)}(x_2) + O(h^4)
\end{aligned}
$$

$$\implies$$
$$
\begin{aligned}
    f'(x_2) - L_2'(x_2) &= f'(x_2) -\frac{1}{2h} \lbrack 2h f'(x_2) - \frac{2}{3} h^3f^{(3)}(x_2) + O(h^4) \rbrack \\
    &= \frac{1}{3} h^2 f^{(3)}(x_2) + O(h^3)
\end{aligned}
$$

---

法二: 注意到$L_2(x)$是对$x_0,x_1,x_2$三点进行Lagrange插值的二次多项式, 故有
$$
\begin{aligned}
    f(x) - L_2(x) &= \frac{f^{(3)}(\xi(x))}{3!} (x-x_0)(x-x_1)(x-x_2) \\
    f'(x) - L_2'(x) &= \frac{f^{(4)}(\xi(x))\xi'(x)}{3!} (x-x_0)(x-x_1)(x-x_2) + \frac{f^{(3)}(\xi(x))}{3!} (x-x_1)(x-x_2) \\
    &+ \frac{f^{(3)}(\xi(x))}{3!} (x-x_0)(x-x_2) + \frac{f^{(3)}(\xi(x))}{3!} (x-x_0)(x-x_1)
\end{aligned}
$$

所以$f'(x_0) - L_2'(x_0) = \frac{h^2}{3}f^{(3)}(\xi(x_0)), f'(x_2) - L_2'(x_2) = \frac{h^2}{3}f^{(3)}(\xi(x_2))$
