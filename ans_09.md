# 课后作业9

#### 1. 给定函数$f(x)$离散值如下, 分别用复化梯形和复化Simpson公式计算$\int_{1.0}^{1.8}f(x)dx$. (6分)
|        |     |     |     |     |     |
|:------:|:---:|:---:|:---:|:---:|:---:|
|   $x$  | 1.0 | 1.2 | 1.4 | 1.6 | 1.8 |
| $f(x)$ | 3.0 | 3.6 | 4.5 | 5.2 | 5.0 |

解: 可以看到这里对积分区间做了4等分, 其对应的复化梯形公式为 (课本118页, 6.6式)
$$
\begin{aligned}
    T_4(f) &= h\lbrack \frac{1}{2}f(a) + \sum\limits_{i=1}^3 f(a+ih) + \frac{1}{2}f(b) \rbrack \\
           &= 0.2\lbrack \frac{1}{2}f(1.0) + \sum\limits_{i=1}^3 f(1.0+0.2i) + \frac{1}{2}f(1.8) \rbrack \\
           &= 0.2\lbrack \frac{1}{2} \times 3.0 + 3.6 + 4.5 + 5.2 + \frac{1}{2} \times 5.0 \rbrack \\
           &= 3.46
\end{aligned}
$$

4等分区间对应的复化Simpson公式为 (课本119页, 6.8式)
$$
\begin{aligned}
    S_4(f) &= \frac{h}{3}\lbrack f(a) + 4\sum\limits_{i=0}^{2-1}f(x_{2i+1}) + 2\sum\limits_{i=1}^{2-1}f(x_{2i}) + f(b) \rbrack \\
           &= \frac{0.2}{3}\lbrack f(1.0) + 4f(1.2) + 2f(1.4) + 4f(1.6) + f(1.8) \rbrack \\
           &= \frac{0.2}{3}\lbrack 3.0 + 4 \times 3.6 + 2 \times 4.5 + 4 \times 5.2 + 5.0 \rbrack \\
           &= 3.48
\end{aligned}
$$

---

#### 2. 给定函数$f(x)$的离散值表, 分别用向前、向后及中心差商公式计算$f'(0.02), f'(0.04)$. (6分)
|        |     |      |      |      |
|:------:|:---:|:----:|:----:|:----:|
|   $x$  | 0.0 | 0.02 | 0.04 | 0.06 |
| $f(x)$ | 6.0 |  4.0 |  2.0 |  5.0 |

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

|            | 向前差商                                   | 向后差商                                 | 中心差商                                  |
|------------|--------------------------------------------|------------------------------------------|-------------------------------------------|
| $f'(0.02)$ | $\frac{f(0.04)-f(0.02)}{0.04-0.02}=-100.0$ | $\frac{f(0.02)-f(0.0)}{0.02-0.0}=-100.0$ | $\frac{f(0.04)-f(0.0)}{0.04-0.0}=-100.0$  |
| $f'(0.04)$ | $\frac{f(0.06)-f(0.04)}{0.06-0.04}=150.0$  | $\frac{f(0.04)-f(0.02)}{0.04-0.02}=-100$ | $\frac{f(0.06)-f(0.02)}{0.06-0.02}=25.0$ |

---

#### 3. 试推导积分$\int_0^2 (x-1)^2 f(x)dx$的2点Gauss积分公式, 这里$(x-1)^2$为权重函数. (10分)

解: 注意这一题是带**权重函数**的Gauss积分, **不能**直接套书上关于Gauss-Legendre积分的公式

求解Gauss积分的三个步骤,

1. 求出区间$[a, b]$上权函数为$W(x)$的正交多项式$p_n(x) \perp \mathbb{P}_{n-1}$.
2. 求出$p_n(x)$的$n$个零点${x_1,x_2,\cdots,x_n}$即为Gauss积分节点.
3. 计算积分系数$\alpha_i=\int_a^b W(x)l_i(x)dx$.

Gauss积分公式即为,
$$
G_n(f) = \sum\limits_{i=1}^n \alpha_i f(x_i)
$$

注意这里的正交性由关于权函数的内积定义,
$$
(f, g) \triangleq \int_a^b W(x)f(x)g(x)dx, \qquad f(x) \perp g(x) \Leftrightarrow (f, g) = 0
$$

下面按照上述三步骤求解Gauss积分:

**步骤一**
$$ p_0(x) = 1 $$
$$ p_1(x) = x - \frac{(x, p_0(x))}{(p_0(x), p_0(x))} p_0(x) = x - 1 $$
其中, $(x, p_0(x)) = \int_0^2 (x-1)^2 x dx = \frac{2}{3},\ (p_0(x), p_0(x)) = \int_0^2 (x-1)^2 dx = \frac{2}{3}$
$$ p_2(x) = x^2 - \frac{(x^2, p_0(x))}{(p_0(x), p_0(x))}p_0(x) - \frac{(x^2, p_1(x))}{(p_1(x), p_1(x))}p_1(x) = x^2 - 2x + \frac{2}{5} $$
其中, $(x^2, p_0(x)) = \int_0^2 (x-1)^2 x^2 dx = \frac{16}{15},\ (x^2, p_1(x)) = \int_0^2 (x-1)^3 x^2 dx = \frac{4}{5}$
$(p_1(x), p_1(x)) = \int_0^2 (x - 1)^4 dx = \frac{2}{5}$

&nbsp;

**步骤二**

求解$p_2(x)$的两个零点$\implies\ x_0 = 1 + \frac{\sqrt{15}}{5} = 1.774597,\ x_1 = 1 - \frac{\sqrt{15}}{5} = 0.225403$

&nbsp;

**步骤三**

Gauss积分系数为,
$$
\begin{aligned}
    \alpha_0 &= \int_0^2 (x-1)^2 \frac{x - x_1}{x_0 - x_1} dx = \frac{1}{3} \\
    \alpha_1 &= \int_0^2 (x-1)^2 \frac{x - x_0}{x_1 - x_0} dx = \frac{1}{3}
\end{aligned}
$$

最后得到Gauss积分公式为,
$$ G_2(f) = \frac{1}{3} f(1 + \frac{\sqrt{15}}{5}) + \frac{1}{3} f(1 - \frac{\sqrt{15}}{5}) $$

法二: 作$y=x-1$的变换, 积分变为(其中$g(y) = f(y+1)$)
$$
\int_0^2 (x-1)^2 f(x)dx = \int_{-1}^1 y^2 g(y) dy
$$

**步骤一**
$$ p_0(y) = 1 $$
$$ p_1(y) = y - \frac{(y, p_0(y))}{(p_0(y), p_0(y))} p_0(y) = y$$
其中, $(y, p_0(y)) = \int_{-1}^1 y^3 dy = 0$
$$ p_2(y) = y^2 - \frac{(y^2, p_0(y))}{(p_0(y), p_0(y))}p_0(y) - \frac{(y^2, p_1(y))}{(p_1(y), p_1(y))}p_1(y) = y^2 - \frac{3}{5} $$
其中,
$$(y^2, p_0(y)) = \int_{-1}^1 y^4 dy = \frac{2}{5}$$
$$(p_0(y), p_0(y)) = \int_{-1}^1 y^2 dy = \frac{2}{3}$$
$$(y^2, p_1(y)) = \int_{-1}^1 y^5 dy = 0$$

&nbsp;

**步骤二**

求解$p_2(y)$的两个零点$\implies\ y_0 = \frac{\sqrt{15}}{5},\ y_1 = - \frac{\sqrt{15}}{5}$

&nbsp;

**步骤三**

Gauss积分系数为,
$$
\begin{aligned}
    \alpha_0 &= \int_{-1}^1 y^2 \frac{y - y_1}{y_0 - y_1} dy = \frac{1}{3} \\
    \alpha_1 &= \int_{-1}^1 y^2 \frac{y - y_0}{y_1 - y_0} dy = \frac{1}{3}
\end{aligned}
$$

最后得到Gauss积分公式为,
$$ G_2(g) = \frac{1}{3} g(\frac{\sqrt{15}}{5}) + \frac{1}{3} g(\frac{\sqrt{15}}{5}) $$
$$ G_2(f) = \frac{1}{3} f(1 + \frac{\sqrt{15}}{5}) + \frac{1}{3} f(1 - \frac{\sqrt{15}}{5}) $$

---

#### 4. 设函数$f(x)$充分光滑(可微), 试推导如下数值微分公式(即确定常数A, B, C, D, E), 使其截断误差为$O(h^4)$, 其中$h>0$ (10分)
$$ f'(x) \approx \frac{1}{h}[Af(x-2h) + Bf(x-h) + Cf(x) + Df(x+h) + Ef(x+2h)] $$

解: 将$f(x-2h), f(x-h), f(x+h), f(x+2h)$分别在$x$点处Taylor展开, 得
$$
\begin{aligned}
    f(x-2h) &= f(x) - 2hf'(x) + 2h^2 f''(x) - \frac{4}{3}h^3 f^{(3)}(x) + \frac{2}{3}h^4 f^{(4)}(x) + O(h^5) \\
    f(x-h) &= f(x) -hf'(x) + \frac{1}{2}h^2 f''(x) - \frac{1}{6}h^3 f^{(3)}(x) + \frac{1}{24}h^4 f^{(4)}(x) + O(h^5) \\
    f(x+h) &= f(x) +hf'(x) + \frac{1}{2}h^2 f''(x) + \frac{1}{6}h^3 f^{(3)}(x) + \frac{1}{24}h^4 f^{(4)}(x) + O(h^5) \\
    f(x+2h) &= f(x) + 2hf'(x) + 2h^2 f''(x) + \frac{4}{3}h^3 f^{(3)}(x) + \frac{2}{3}h^4 f^{(4)}(x) + O(h^5)
\end{aligned}
$$

数值微分公式两端各项系数应该相等, 可列出关于$A, B, C, D, E$的五个方程
$$
\left\{
\begin{aligned}
    A + B + C + D + E &= 0 \ \ \ (1)\\
    -2A -B + D + 2E &= 1 \ \ \ (2)\\
    2A + \frac{1}{2}B + \frac{1}{2}D + 2E &= 0 \ \ \ (3)\\
    -\frac{4}{3}A -\frac{1}{6}B + \frac{1}{6}D + \frac{4}{3}E &= 0 \ \ \ (4) \\
    \frac{2}{3}A + \frac{1}{24}B + \frac{1}{24}D + \frac{2}{3}E &= 0 \ \ \ (5)
\end{aligned}
\right.
$$

从(3)和(5)可看出$A=-E,\ B=-D$, 在结合(1)可知$C=0$, 此时重新整理一下(2)和(4)
$$
\left\{
\begin{aligned}
    -4A -2B &= 1 \ \ \ (2)\\
    -\frac{8}{3}A -\frac{1}{3}B &= 0 \ \ \ (4)
\end{aligned}
\right.
$$

可解出
$$
\left\{
\begin{aligned}
    A = \frac{1}{12} \\
    B = -\frac{2}{3} \\
    C = 0 \\
    D = \frac{2}{3} \\
    E = -\frac{1}{12} \\
\end{aligned}
\right.
$$

故而
$$ f'(x) \approx \frac{1}{h}[\frac{1}{12}f(x-2h) - \frac{2}{3}f(x-h) + \frac{2}{3}f(x+h) - \frac{1}{12}f(x+2h)] $$

---

法二: 记$x_0 = x$, $x_1 = x - 2h$, $x_2 = x - h$, $x_3 = x + h$, $x_4 = x + 2h$
以$x_0,\cdots, x_4$ 为节点构造Lagrange插值多项式
$$
\begin{aligned}
    l_0(x) &= \frac{(x-x_1)(x-x_2)(x-x_3)(x-x_4)}{(x_0-x_1)(x_0-x_2)(x_0-x_3)(x_0-x_4)} \\
           &= \frac{1}{4h^4}[(x-x_0)^4 - 5h^2 (x-x_0)^2 + 4h^2]  \\
    l_1(x) &= \frac{(x-x_0)(x-x_2)(x-x_3)(x-x_4)}{(x_1-x_0)(x_1-x_2)(x_1-x_3)(x_1-x_4)} \\
           &= \frac{1}{24h^4}[(x-x_0)^4 - 2h(x-x_0)^3 - h^2(x-x_0)^2 + 2h^3(x-x_0)]  \\
    l_2(x) &= \frac{(x-x_0)(x-x_1)(x-x_3)(x-x_4)}{(x_2-x_0)(x_2-x_1)(x_2-x_3)(x_2-x_4)} \\
           &= -\frac{1}{6h^4}[(x-x_0)^4 - h(x-x_0)^3 - 4h^2(x-x_0)^2 + 4h^3(x-x_0)]  \\
    l_3(x) &= \frac{(x-x_0)(x-x_1)(x-x_2)(x-x_4)}{(x_3-x_0)(x_3-x_1)(x_3-x_2)(x_3-x_4)} \\
           &= -\frac{1}{6h^4}[(x-x_0)^4 + h(x-x_0)^3 - 4h^2(x-x_0)^2 - 4h^3(x-x_0)]  \\
    l_4(x) &= \frac{(x-x_0)(x-x_1)(x-x_2)(x-x_3)}{(x_4-x_0)(x_4-x_1)(x_4-x_2)(x_4-x_3)} \\
           &= \frac{1}{24h^4}[(x-x_0)^4 + 2h(x-x_0)^3 - h^2(x-x_0)^2 - 2h^3(x-x_0)]  \\
\end{aligned}
$$

所以
$$
\begin{aligned}
    L_4(x) &= l_0(x)f(x_0) + l_1(x)f(x_1) + l_2(x)f(x_2) + l_3(x)f(x_3) + l_4(x)f(x_4) \\
    L_4'(x) &= l_0'(x)f(x_0) + l_1'(x)f(x_1) + l_2'(x)f(x_2) + l_3'(x)f(x_3) + l_4'(x)f(x_4) \\
\end{aligned}
$$

对插值基函数分别求导得
$$
\begin{aligned}
    l_0'(x) &= \frac{1}{4h^4}[4(x-x_0)^3 - 10h^2(x-x_0)] \\
    l_1'(x) &= \frac{1}{24h^4}[4(x-x_0)^3 -6h(x-x_0)^2 - 2h^2(x-x_0) + 2h^3] \\
    l_2'(x) &= -\frac{1}{6h^4}[4(x-x_0)^3 - 3h(x-x_0)^2 - 8h^2(x-x_0) + 4h^3] \\
    l_3'(x) &= -\frac{1}{6h^4}[4(x-x_0)^3 + 3h(x-x_0)^2 - 8h^2(x-x_0) - 4h^3] \\
    l_4'(x) &= \frac{1}{24h^4}[4(x-x_0)^3 +6h(x-x_0)^2 - 2h^2(x-x_0) - 2h^3] \\
\end{aligned}
$$

代入$x_0$得, $l_0'(x_0) = 0$, $l_1'(x_0) = \frac{1}{12h}$, $l_2'(x_0) = -\frac{2}{3h}$, $l_3'(x_0) = \frac{2}{3h}$, $l_4'(x_0) = -\frac{1}{12h}$

所以
$$
L_4'(x_0) = \frac{1}{h}[\frac{1}{12}f(x_0-2h) - \frac{2}{3}f(x_0-h) + \frac{2}{3}f(x_0+h) - \frac{1}{12}f(x_0+2h)]
$$

将$x_0$改写成$x$即可得
$$ f'(x) \approx L_4'(x) = \frac{1}{h}[\frac{1}{12}f(x-2h) - \frac{2}{3}f(x-h) + \frac{2}{3}f(x+h) - \frac{1}{12}f(x+2h)] $$
$$ \implies A=\frac{1}{12}, B=-\frac{2}{3}, C=0, D=\frac{2}{3}, E=-\frac{1}{12}$$

由Lagrange插值函数误差公式
$$
f'(x) - L_4'(x) = (\frac{f^{(5)}(\xi_x)}{5!}(x-x_0)(x-x_1)(x-x_2)(x-x_3)(x-x_4))'
$$

代入$x=x_0$, 只保留了一项
$$
f'(x_0) - L_4'(x_0) = \frac{f^{(5)}(\xi_{x_0})}{5!}(x_0-x_1)(x_0-x_2)(x_0-x_3)(x_0-x_4) = \frac{h^4}{30} f^{(5)}(\xi_{x_0})
$$
