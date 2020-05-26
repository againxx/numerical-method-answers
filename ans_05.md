# 课后作业5

#### 1. 给定$n>1$, 给出牛顿法计算$\sqrt[n]{a}\;(a>0)$时的迭代公式, 并用此公式来计算$\sqrt[5]{9}$, 取初值$x_0 = 2$, 迭代3次, 求$x_3$. (5分)
解: 令$f(x) = x^n - a$, $f(x)$的根为$\sqrt[n]{a}$, 由牛顿迭代公式
$$
x_{k+1} = x_k - \frac{f(x_k)}{f'(x_k)} = x_k - \frac{x_k^n - a}{n x_k^{n-1}}
$$
代入$n = 5, a = 9, x_0 = 2$
$$
\begin{aligned}
    x_1 &= x_0 - \frac{x_0^5 - 9}{5 x_0^4} = 1.71250 \\
    x_2 &= x_1 - \frac{x_1^5 - 9}{5 x_1^4} = 1.57929 \\
    x_3 &= x_2 - \frac{x_2^5 - 9}{5 x_2^4} = 1.55278
\end{aligned}
$$

---

#### 2. 写出对方程$x^3 - 4x^2 + 5x - 2 = 0$求根时的Newton迭代公式$x_n = \varphi(x_n - 1)$. 取初值$x_0 = 0$, 判断极限$\lim\limits_{n \to \infty}x_n$是否存在; 请给出你的理由或证明. (10分)
解: 牛顿迭代公式为,
$$
x_n = x_{n-1} - \frac{x_{n-1}^3 - 4x_{n-1}^2 + 5x_{n-1} - 2}{3x_{n-1}^2 - 8x_{n-1} + 5}
= x_{n-1} - \frac{(x_{n-1} - 1)(x_{n-1} - 2)}{3x_{n-1} - 5}
$$
$$
\Rightarrow
\varphi(x) = x - \frac{(x - 1)(x - 2)}{3x - 5}
$$
推测$x=1$或$x=2$可能是不动点

---

**法一**:
$$
\varphi(x_0) = x_0 - \frac{(x_0 - 1)(x_0 - 2)}{3x_0 - 5} = \frac{2}{5}
$$
$$
\varphi'(x) = \frac{f(x)f''(x)}{(f'(x))^2} = \frac{(x^3 - 4x^2 + 5x -2)(6x - 8)}{(3x^2 - 8x + 5)^2}
\Rightarrow
\varphi'(x_0) = \frac{16}{25}
$$
进一步化简, 得到
$$
1 - \varphi(x) = 1 - x - \frac{(1 - x)(x - 2)}{3x - 5} = (1 - x)\frac{2x - 3}{3x - 5}
$$
当$0 \leq x \leq 1$时, 
$$
\frac{1}{2} \leq \frac{2x - 3}{3x - 5} \leq \frac{3}{5}
\Rightarrow
0 \leq 1 - \varphi(x) \leq 1
\Rightarrow
0 \leq \varphi(x) \leq 1
$$
于是当$n \geq 1, 0 \leq x_{n-1} \leq 1$时, 迭代得到的下一项$0 \leq x_n \leq 1$

由$x_n = \varphi(x_{n-1})$知,
$$
\begin{aligned}
    0 \leq 1 - x_n \leq 1 - \varphi(x_{n-1}) &= (1 - x_{n-1})\frac{2x_{n-1} - 3}{3x_{n-1} - 5} \\
    &\leq (1 - x_{n-1})\times\frac{3}{5} \\
    &\leq(1 - x_{n-2})\times(\frac{3}{5})^2 \\
    &\leq(1 - x_0)\times(\frac{3}{5})^n = (\frac{3}{5})^n
\end{aligned}
$$
当$n \rightarrow +\infty$时, $\lim\limits_{n \rightarrow +\infty} x_n = 1$

---

**法二**:

注意到,
$$
\varphi'(x) = \frac{6x^2 - 20x + 16}{(3x - 5)^2} = \frac{(x - 2)(6x - 8)}{(3x - 5)^2}
$$
则$\varphi(x)$的极值点位于$x=\frac{4}{3}$和$x=2$, 于是$\varphi(x)$在$x \in [0, 1]$时单调递增且连续,
又因为$\varphi(0) = \frac{2}{5}, \varphi(1) = 1$, 于是 $x \in [0, 1]$时, $0 \leq \varphi(x) \leq 1$

求$\varphi(x)$的二阶导数
$$
\varphi''(x) = \frac{4}{(3x - 5)^3}
$$
知$x \in [0, 1]$时, $\varphi''(x) < 0$, 于是$\varphi'(x)$在$[0, 1]$上单调递增

而$\varphi'(0) = \frac{16}{25}, \varphi'(1) = \frac{1}{2}$, 所以, $x \in [0, 1]$时 $\lvert\varphi'(x)\rvert \leq \frac{16}{25} \lt 1$

由压缩映射定理知, 在$[0, 1]$区间上, $\varphi(x)$必有唯一的不动点, 即$x=1$
