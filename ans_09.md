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

|            | 向前差商                                   | 向后差商                                 | 中心差商                                  |
|------------|--------------------------------------------|------------------------------------------|-------------------------------------------|
| $f'(0.02)$ | $\frac{f(0.04)-f(0.02)}{0.04-0.02}=-100.0$ | $\frac{f(0.02)-f(0.0)}{0.02-0.0}=-100.0$ | $\frac{f(0.04)-f(0.0)}{0.04-0.0}=-100.0$  |
| $f'(0.04)$ | $\frac{f(0.06)-f(0.04)}{0.06-0.04}=300.0$  | $\frac{f(0.04)-f(0.02)}{0.04-0.02}=-100$ | $\frac{f(0.06)-f(0.02)}{0.06-0.02}=100.0$ |

---

#### 2. 求积分$\int_0^1 x^2 f(x)dx$的2点Gauss积分公式, 这里$x^2$为权重函数. (6分)

解: 注意这一题是带权重函数的Gauss积分, 不能直接套书上的公式

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
$$ p_1(x) = x - \frac{(x, p_0(x))}{(p_0(x), p_0(x))} p_0(x) = x - \frac{3}{4} $$
其中, $(x, p_0(x)) = \int_0^1 x^3 dx = \frac{1}{4},\ (p_0(x), p_0(x)) = \int_0^1 x^2 dx = \frac{1}{3}$
$$ p_2(x) = x^2 - \frac{(x^2, p_0(x))}{(p_0(x), p_0(x))}p_0(x) - \frac{(x^2, p_1(x))}{(p_1(x), p_1(x))}p_1(x) = x^2 - \frac{4}{3} + \frac{2}{5} $$
其中, $(x^2, p_0(x)) = \int_0^1 x^4 dx = \frac{1}{5},\ (x^2, p_1(x)) = \int_0^1 x^5 - \frac{3}{4}x^4dx = \frac{1}{60}$
$(p_1(x), p_1(x)) = \int_0^1 x^2(x - \frac{3}{4})^2 dx = \frac{1}{80}$

&nbsp;

**步骤二**

求解$p_2(x)$的两个零点$\implies\ x_0 = \frac{2}{3} + \frac{\sqrt{10}}{15} = 0.87749,\ x_1 = \frac{2}{3} - \frac{\sqrt{10}}{15} = 0.45585$

&nbsp;

**步骤三**

Gauss积分系数为,
$$
\begin{aligned}
    \alpha_0 &= \int_0^1 x^2 \frac{x - x_1}{x_0 - x_1} dx = \frac{8 + \sqrt{10}}{48} = 0.23255 \\
    \alpha_1 &= \int_0^1 x^2 \frac{x - x_0}{x_1 - x_0} dx = \frac{8 - \sqrt{10}}{48} = 0.10079
\end{aligned}
$$

最后得到Gauss积分公式为,
$$ G_2(f) = 0.23255 f(0.87749) + 0.10079 f(0.45585) $$

---

#### 3. 设有常微分初值问题
$$
\left\{
\begin{aligned}
    y'(x) &= -y(x), (0 \leq x \leq 1) \\
    y(0)  &= 1
\end{aligned}
\right.
$$
假设求解区间$[0,1]$被$n$等分($n$充分大), 令$h = \frac{1}{n}, x_k = \frac{k}{n} (k=0,1,\cdots,n)$,

(a) 分别写出用**向前Euler公式**, **向后Euler公式**, **梯形格式**以及**改进的Euler公式**求上述微分方程数值解时的差分公式
(即分别写出此四种方法/公式下, $y_{k+1}$与$y_k$之间的递推关系式). (4分, 每种方法给1分)

(b) 设$y_0 = y(0)$, 分别求此四种公式(方法)下的近似值$y_n$的表达式; (注: 这里的$y_n$即是$y(x_n) \equiv y(1)$的近似值). (4分, 每种方法给1分)

\(c\) 当$n$充分大(即区间长度$h \rightarrow 0$)时, 分别判断四种方法下的近似值$y_n$是否收敛到原问题的真解$y(x)$在$x=1$处的值(i.e., $y(1)$).
(8分, 每种方法给2分)

&nbsp;

解: (a)

向前Euler公式为
$$ y_{k+1} = y_k + hf(x_k, y_k) = y_k - \frac{1}{n} y_k = (1 - \frac{1}{n}) y_k $$

向后Euler公式为
$$ y_{k+1} = y_k + hf(x_{k+1}, y_{k+1}) = y_k - \frac{1}{n} y_{k+1} \implies y_{k+1} = (1 - \frac{1}{n+1}) y_k $$

梯形格式为
$$
\begin{aligned}
    & y_{k+1} = y_k + \frac{h}{2}(f(x_k, y_k) + f(x_{k+1}, y_{k+1})) = y_k - \frac{1}{2n}(y_k + y_{k+1}) \\
    & \implies y_{k+1} = (1 - \frac{2}{2n+1}) y_k
\end{aligned}
$$

改进的Euler公式为
$$
\begin{aligned}
    y_{k+1} &= y_k + \frac{h}{2}(f(x_k, y_k) + f(x_{k+1}, y_k + hf(x_k, y_k))) \\
            &= y_k + \frac{1}{2n}(-y_k + (-y_k+\frac{1}{n}(-y_k))) \\
    \implies & y_{k+1} = (1 - \frac{1}{n} + \frac{1}{2n^2}) y_k
\end{aligned}
$$

(b) 由(a)中的$y_{k+1}$与$y_k$之间的递推关系式, 以及$y_0 = 1$

向前Euler公式
$$ y_n = (1 - \frac{1}{n})^n y_0 = (1 - \frac{1}{n})^n $$

向后Euler公式
$$ y_n = (1 - \frac{1}{n+1})^n y_0 = (1 - \frac{1}{n+1})^n $$

梯形公式
$$ y_n = (1 - \frac{2}{2n+1})^n y_0 = (1 - \frac{2}{2n+1})^n $$

改进Euler公式
$$ y_n = (1 - \frac{1}{n} + \frac{1}{2n^2})^n y_0 = (1 - \frac{1}{n} + \frac{1}{2n^2})^n $$

\(c\) 易知原方程的解析解为$y(x) = e^{-x}$, 则真解$y(1) = \frac{1}{e}$, 下面验证$n \rightarrow \infty$时, 四种方法下近似值$y_n$的收敛性

向前Euler公式
$$ \lim_{n \rightarrow \infty} y_n = \lim_{n \rightarrow \infty} (1 - \frac{1}{n})^n = \frac{1}{e} $$

向后Euler公式
$$ \lim_{n \rightarrow \infty} y_n = \lim_{n \rightarrow \infty} (1 - \frac{1}{n+1})^n
= \lim_{n \rightarrow \infty} (1 - \frac{1}{n+1})^{(n+1) \times \frac{n}{n+1}} = \frac{1}{e}$$

梯形公式
$$ \lim_{n \rightarrow \infty} y_n = \lim_{n \rightarrow \infty} (1 - \frac{2}{2n+1})^n
= \lim\limits_{n \rightarrow \infty} (1 - \frac{2}{2n+1})^{\frac{2n+1}{2} \times \frac{2n}{2n+1}} = \frac{1}{e}$$

改进Euler公式
$$
\begin{aligned}
    \lim\limits_{n \rightarrow \infty} y_n &= \lim\limits_{n \rightarrow \infty}(1 - \frac{1}{n} + \frac{1}{2n^2})^n
    = \lim\limits_{n \rightarrow \infty}(1 - \frac{2n-1}{2n^2})^n \\
    &= \lim\limits_{n \rightarrow \infty}(1 - \frac{2n-1}{2n^2})^{\frac{2n^2}{2n-1} \times \frac{2n^2-n}{2n^2}}
    = \frac{1}{e}
\end{aligned}
$$
