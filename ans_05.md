# 课后作业5

#### 1. 给出下列数据, 用最小二乘法求形如$y = ae^{bx}$的经验公式. (5分)
|       |       |       |      |      |
|:-----:|:-----:|:-----:|:----:|:----:|
| $x_i$ | 0.25 | 0.50 | 0.60 | 0.75 |
| $y_i$ | 1.00  | 1.25  | 2.45 | 4.25 |
解: 对$y = ae^{bx}$两端同时作用对数函数得到, $\ln{y} = \ln{a} + bx$  
令$z_i = \ln{y_i}$, 可得离散数据$\{(x_i, z_i)\}_{i=1}^4$

|       |       |       |      |      |
|:-----:|:-----:|:-----:|:----:|:----:|
| $x_i$ | 0.25 | 0.50 | 0.60 | 0.75 |
| $z_i$ | 0.0  | 0.223144 | 0.896088 | 1.446919 |

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
    4 & 2.1 \\
    2.1 & 1.235
\end{pmatrix}
\begin{pmatrix}
    A \\
    B
\end{pmatrix}
=
\begin{pmatrix}
    2.566151 \\
    1.734414
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
    -0.8925894 \\
    2.922147
\end{pmatrix}
$$
得到 $a = e^A = 0.409594 \quad b = B = 2.922147$

即 $y = 0.409594e^{2.922147x}$

---

#### 2. 给定$n>1$, 给出用牛顿法计算$\sqrt[n]{a}\;(a>0)$时的迭代公式, 并用此公式来计算$\sqrt[5]{9}$, 取初值$x_0 = 2$, 迭代5次, 求$x_5$. (5分)
解: 令$f(x) = x^n - a$, $f(x)$的根为$\sqrt[n]{a}$, 由牛顿迭代公式 (课本65页, 式3.2)
$$
x_{k+1} = x_k - \frac{f(x_k)}{f'(x_k)} = x_k - \frac{x_k^n - a}{n x_k^{n-1}}
$$
代入$n = 5, a = 9, x_0 = 2$
$$
\begin{aligned}
    x_1 &= x_0 - \frac{x_0^5 - 9}{5 x_0^4} = 1.71250 \\
    x_2 &= x_1 - \frac{x_1^5 - 9}{5 x_1^4} = 1.57929 \\
    x_3 &= x_2 - \frac{x_2^5 - 9}{5 x_2^4} = 1.55278 \\
    x_4 &= x_3 - \frac{x_3^5 - 9}{5 x_3^4} = 1.55185 \\
    x_5 &= x_4 - \frac{x_4^5 - 9}{5 x_4^4} = 1.55185
\end{aligned}
$$

---

#### 3. 写出对方程$x^3 - 4x^2 + 5x - 2 = 0$求根时的Newton迭代公式$x_n = \varphi(x_n - 1)$. 取初值$x_0 = 0$, 判断极限$\lim\limits_{n \to \infty}x_n$是否存在; 请给出你的理由或证明. (10分)
解: 牛顿迭代公式为,
$$
x_n = x_{n-1} - \frac{x_{n-1}^3 - 4x_{n-1}^2 + 5x_{n-1} - 2}{3x_{n-1}^2 - 8x_{n-1} + 5}
= x_{n-1} - \frac{(x_{n-1} - 1)(x_{n-1} - 2)}{3x_{n-1} - 5}
$$
$$
\implies
\varphi(x) = x - \frac{(x - 1)(x - 2)}{3x - 5} = \frac{2(x^2 - x - 1)}{3x - 5}
$$
若极限$\lim\limits_{n \to \infty} x_n = x^*$存在, 则 $\varphi(x^*) = x^*$

推测$x^*=1$或$x^*=2$可能是不动点

---

**法一** : 尝试证明$\lim\limits_{n \to \infty} (1 - \varphi(x_n)) = 0$

对 $1 - \varphi(x)$ 进行化简, 得到
$$
1 - \varphi(x) = 1 - x - \frac{(1 - x)(x - 2)}{3x - 5} = \frac{(1 - x)(2x - 3)}{3x - 5}
$$
当$0 \leq x \leq 1$时, (注意$x_0 = 0$)
$$
\frac{1}{2} \leq \frac{2x - 3}{3x - 5} \leq \frac{3}{5}
\implies
0 \leq 1 - \varphi(x) \leq 1
\implies
0 \leq \varphi(x) \leq 1
$$
于是当$n \geq 1, 0 \leq x_{n-1} \leq 1$时, 迭代得到的下一项$0 \leq x_n \leq 1$

由$x_n = \varphi(x_{n-1})$知,
$$
\begin{aligned}
    0 \leq 1 - x_n = 1 - \varphi(x_{n-1}) &= \frac{(1 - x_{n-1})(2x_{n-1} - 3)}{3x_{n-1} - 5} \\
    &\leq (1 - x_{n-1})\times\frac{3}{5} \\
    &\leq(1 - x_{n-2})\times(\frac{3}{5})^2 \\
    &\leq(1 - x_0)\times(\frac{3}{5})^n = (\frac{3}{5})^n
\end{aligned}
$$
当$n \to +\infty$时, $\lim\limits_{n \to +\infty} x_n = 1$

---

**法二** : 利用压缩映射定理 (课本62页, 定理3.1), 需要满足两个条件

1. 当$x \in [a,b]$时, 有$a \leq \varphi(x) \leq b$
2. $\varphi(x)$在$[a,b]$上可导, 并且存在正数$L < 1$, 使对任意的$x \in [a,b]$, 有$| \varphi'(x) | \leq L$

注意到,
$$
\varphi'(x) = \frac{f(x)f''(x)}{(f'(x))^2} = \frac{(x^3 - 4x^2 + 5x -2)(6x - 8)}{(3x^2 - 8x + 5)^2}
= \frac{(x - 2)(6x - 8)}{(3x - 5)^2}
$$

则$\varphi(x)$的极值点位于$x=\frac{4}{3}$和$x=2$, 于是$\varphi(x)$在$x \in [0, 1]$时单调递增且连续,
又因为$\varphi(0) = \frac{2}{5}, \varphi(1) = 1$, 于是 $x \in [0, 1]$时, $0 \leq \varphi(x) \leq 1$

为了估计$\varphi'(x)$的范围, 接下来求$\varphi(x)$的二阶导数
$$
\varphi''(x) = \frac{4}{(3x - 5)^3}
$$
知$x \in [0, 1]$时, $\varphi''(x) < 0$, 于是$\varphi'(x)$在$[0, 1]$上单调递减

而$\varphi'(0) = \frac{16}{25}, \varphi'(1) = \frac{1}{2}$, 所以, $x \in [0, 1]$时 $\lvert\varphi'(x)\rvert \leq \frac{16}{25} \lt 1$

由压缩映射定理知, 在$[0, 1]$区间上, $\varphi(x)$必有唯一的不动点, 即$x=1$
