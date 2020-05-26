# 课后作业02

#### 1. $f(x) = \sqrt{x}$ 在离散点有$f(81) = 9$, $f(100) = 10$, $f(121) = 11$, 用插值方法计算$\sqrt{108}$的近似值, 根据误差公式给出误差界. (5分)

解: 用Lagrange插值多项式
$$
\begin{aligned}
    l_0(x) &= \frac{(x - 100)(x - 121)}{(81 - 100)(81 - 121)} = \frac{1}{760}(x - 100)(x - 121) \\
    l_1(x) &= \frac{(x - 81)(x - 121)}{(100 - 81)(100 - 121)} = -\frac{1}{399}(x - 81)(x - 121) \\
    l_2(x) &= \frac{(x - 81)(x - 100)}{(121 - 81)(121 - 100)} = \frac{1}{840}(x - 81)(x - 100) \\
    L_2(x) &= \frac{9}{760}(x - 100)(x - 121) - \frac{10}{399}(x - 81)(x - 121) + \frac{11}{840}(x - 81)(x - 100) \\
\end{aligned}
$$
$$
\begin{aligned}
    L_2(108) &= \frac{9}{760} \times 8 \times (-13) - \frac{10}{399} \times 27 \times (-13) + \frac{11}{840} \times 27 \times 8 \\
             &= \frac{6912}{665} = 10.393984962 \\
    f(108) &= \sqrt{108} = 10.392304845
\end{aligned}
$$

绝对误差: $R(x) = f(108) - L_2(108) = -0.001680117$

误差公式: $R_2(x) = \frac{f^{(3)}(\xi)}{3!}(x - 81)(x - 100)(x - 121) \qquad \xi \in [81, 121]$

误差界: $R_2(108) = -468 f^{(3)}(\xi) = -\frac{351}{2}\xi^{-\frac{5}{2}} \in [-0.002972108, -0.001089717]$

---

#### 2. 利用下面的函数值表, 作出差商表, 写出相应的牛顿插值多项式, 并计算$f(1.5)$的近似值. (5分)

  |  |  |  |  |  | 
:-: | :-: | :-: | :-: | :-:
$\qquad x \qquad$ | 1.0 | 2.0 | 3.0 | 4.0
$\qquad f(x) \qquad$ | 2.0 | 4.0 | 8.0 | 5.0

解: 

$i$ | $x_i$ | $f(x_i)$ | $f[x_{i-1}, x_i]$ | $f[x_{i-2}, x_{i-1}, x_i]$ | $f[x_{i-3}, x_{i-2}, x_{i-1}, x_i]$
:---|:---:|:---:|:---------:|:----------:|:---:
 0  | 1.0 | 2.0 |
 1  | 2.0 | 4.0 | &ensp;2.0 |
 2  | 3.0 | 8.0 | &ensp;4.0 | &ensp;1.0  |
 3  | 4.0 | 5.0 |      -3.0 |      -3.5  | -1.5

$$
\begin{aligned}
    N_3(x) =& f(x_0) + f[x_0, x_1](x - x_0) + f[x_0, x_1, x_2](x - x_0)(x - x_1) \\
           +& f[x_0, x_1, x_2, x_3](x - x_0)(x - x_1)(x - x_2) \\
           =& 2 + 2(x - 1) + (x - 1)(x - 2) - 1.5(x - 1)(x - 2)(x - 3)
\end{aligned}
$$
$$f(1.5) \approx N_3(1.5) = \frac{35}{16} = 2.1875$$


---

#### 3. 利用数据$f(0)=2.0$, $f(1)=0.5$, $f(3)=0.25$, $f'(3)=0.6$, 并构造出三次插值多项式, 写出其插值余项, 并计算$f(2)$的近似值. (5分)

解: 带导数值的为Hermite插值, 可用类似Lagrange插值或者类似Newton插值的方法求解

方法一(Newton):

$i$ | $x_i$ | $f(x_i)$ | $f[x_{i-1}, x_i]$ | $f[x_{i-2}, x_{i-1}, x_i]$ | $f[x_{i-3}, x_{i-2}, x_{i-1}, x_i]$
:---|:---:|:----:|:------:|:---------------:|:---:
 0  | 0.0 |  2.0 |
 1  | 1.0 |  0.5 |   -1.5 |
 2  | 3.0 | 0.25 | -0.125 | $\frac{11}{24} \approx$ 0.4583 |
 3  | 3.0 | 0.25 |    0.6 | $\frac{29}{80} \approx$ 0.3625 | -$\frac{23}{720} \approx$ -0.031944

得到插值多项式,

$H_3(x) = 2 - \frac{3}{2}x + \frac{11}{24}x(x-1) - \frac{23}{720}x(x-1)(x-3)$

插值余项为,

$$R(x) = f[x,0,1,3,3]x(x-1)(x-3)^2$$

$$f(2) \approx H_3(2) = -\frac{7}{360} = -0.019444$$

方法二(Lagrange):

已知$f(x_0), f(x_1), f(x_2), f'(x_2)$, 设插值多项式$H_3(x)$的基函数为$h_0(x)$, $h_1(x)$, $h_2(x)$, $g_0(x)$, 满足:

$H_3(x) = f(x_0) h_0(x) + f(x_1) h_1(x) + f(x_2) h_2(x) + f'(x_2) g_0(x)$, 并且

$$
\left\{
    \begin{aligned}
        h_0(0) &= 1 \\
        h_0(1) &= 0 \\
        h_0(3) &= 0 \\
        h_0'(3) &= 0
    \end{aligned}
\right.\qquad
\left\{
    \begin{aligned}
        h_1(0) &= 0 \\
        h_1(1) &= 1 \\
        h_1(3) &= 0 \\
        h_1'(3) &= 0
    \end{aligned}
\right.\qquad
\left\{
    \begin{aligned}
        h_2(0) &= 0 \\
        h_2(1) &= 0 \\
        h_2(3) &= 1 \\
        h_2'(3) &= 0
    \end{aligned}
\right.\qquad
\left\{
    \begin{aligned}
        g_0(0) &= 0 \\
        g_0(1) &= 0 \\
        g_0(3) &= 0 \\
        g_0'(3) &= 1
    \end{aligned}
\right.
$$

接下来可推导$h_0(x)$, $h_1(x)$, $h_2(x)$, $g_0(x)$的具体形式
$$
(1)\quad
\begin{aligned}
    h_0(x) &= a_0(x-1)(x-3)^2 \qquad \text{let }x=0 \quad h_0(0) = -9 a_0 = 1 \Rightarrow a_0 = -\frac{1}{9} \\
           &= -\frac{1}{9} (x-1)(x-3)^2
\end{aligned}
$$

$$
(2)\quad
\begin{aligned}
    h_1(x) &= a_1x(x-3)^2 \qquad \text{let }x=1 \quad h_1(1) = 4 a_1 = 1 \Rightarrow a_1 = \frac{1}{4} \\
           &= \frac{1}{4} x(x-3)^2
\end{aligned}
$$

$$
(3)\quad
\left\{
    \begin{aligned}
        h_2(x)  &= x(x-1)(a_2 + b_2 x) \\
        h_2'(x) &= 3b_2 x^2 + 2a_2 x - 2b_2 x - a_2
    \end{aligned}
\right.
\left\{
    \begin{aligned}
        h_2(3)  &= 6(a_2 + 3b_2) = 1 \\
        h_2'(3) &= 5a_2 + 21b_2 = 0
    \end{aligned}
\right. \\
\quad\qquad \Rightarrow a_2 = \frac{7}{12} \quad b_2 = -\frac{5}{36} \quad h_2(x) = x(x-1)(\frac{7}{12} -\frac{5}{36}x)
$$

$$
(4)\quad
\begin{aligned}
    g_0(x) &= a_3 x(x-1)(x-3) \qquad \\
           &= \frac{1}{6}x(x-1)(x-3)
\end{aligned}
\begin{aligned}
    g_0'(x) &= a_3 (3x^2 - 8x + 3) \\
    g_0'(3) &= 6a_3 = 1 \Rightarrow a_3 = \frac{1}{6}
\end{aligned}
$$

得到插值函数,

$$
\begin{aligned}
    H_3(x) &= -\frac{2}{9}(x-1)(x-3)^2 + \frac{1}{8}x(x-3)^2 + \frac{1}{144}x(x-1)(-5x+21) \\
           &+ \frac{1}{10}x(x-1)(x-3)
\end{aligned}
$$

插值余项为,

$$R_3(x) = \frac{f^{(4)}(\xi_x)}{4!}x(x-1)(x-3)^2, \quad \xi_x \in [0,3]$$
$$f(2) \approx H_3(2) = -\frac{7}{360} = -0.019444$$
