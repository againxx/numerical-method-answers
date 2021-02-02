# 课后作业3

#### 1. 利用下面的函数值表, 作出差商表, 写出相应的牛顿插值多项式, 并计算$f(1.5)$的近似值. (6分)

|                      |     |     |     |     |
|:--------------------:|:---:|:---:|:---:|:---:|
|   $\qquad x \qquad$  | 1.0 | 2.0 | 3.0 | 4.0 |
| $\qquad f(x) \qquad$ | 2.0 | 4.0 | 5.0 | 2.0 |

解: 

| $i$ | $x_i$ | $f(x_i)$ | $f[x_{i-1}, x_i]$ | $f[x_{i-2}, x_{i-1}, x_i]$ | $f[x_{i-3}, x_{i-2}, x_{i-1}, x_i]$ |
|:---:|:-----:|:--------:|:-----------------:|:--------------------------:|:-----------------------------------:|
|  0  |  1.0  |    2.0   |                   |                            |                                     |
|  1  |  2.0  |    4.0   |     &ensp;2.0     |                            |                                     |
|  2  |  3.0  |    5.0   |     &ensp;1.0     |            -0.5            |                                     |
|  3  |  4.0  |    2.0   |        -3.0       |            -2.0            |                 -0.5                |

$$
\begin{aligned}
    N_3(x) =& f(x_0) + f[x_0, x_1](x - x_0) + f[x_0, x_1, x_2](x - x_0)(x - x_1) \\
           +& f[x_0, x_1, x_2, x_3](x - x_0)(x - x_1)(x - x_2) \\
           =& 2 + 2(x - 1) - 0.5(x - 1)(x - 2) - 0.5(x - 1)(x - 2)(x - 3)
\end{aligned}
$$
$$f(1.5) \approx N_3(1.5) = \frac{47}{16} = 2.9375$$

---

#### 2. 利用数据$f(0)=2.0$, $f(1)=1.0$, $f(3)=0.25$, $f'(3)=0.6$, 构造出三次插值多项式, 写出其插值余项, 并计算$f(2)$的近似值. (6分)

解: 带导数值的为Hermite插值, 可用类似Lagrange插值或者类似Newton插值的方法求解

方法一 (Newton型):

| $i$ | $x_i$ | $f(x_i)$ | $f[x_{i-1}, x_i]$ |    $f[x_{i-2}, x_{i-1}, x_i]$   | $f[x_{i-3}, x_{i-2}, x_{i-1}, x_i]$ |
|:---:|:-----:|:--------:|:-----------------:|:-------------------------------:|:-----------------------------------:|
|  0  |  0.0  |    2.0   |                   |                                 |                                     |
|  1  |  1.0  |    1.0   |        -1.0       |                                 |                                     |
|  2  |  3.0  |   0.25   |       -0.375      | $\frac{5}{24} \approx$ 0.208333 |                                     |
|  3  |  3.0  |   0.25   |        0.6        |  $\frac{39}{80} \approx$ 0.4875 |  $\frac{67}{720} \approx$ 0.093056  |

得到插值多项式,

$H_3(x) = 2 - x + \frac{5}{24}x(x-1) + \frac{67}{720}x(x-1)(x-3)$

插值余项为,

$$R(x) = f[x,0,1,3,3]x(x-1)(x-3)^2$$

$$f(2) \approx H_3(2) = \frac{83}{360} = 0.230556$$

方法二 (Lagrange型):

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
    H_3(x) &= -\frac{2}{9}(x-1)(x-3)^2 + \frac{1}{4}x(x-3)^2 + \frac{1}{144}x(x-1)(-5x+21) \\
           &+ \frac{1}{10}x(x-1)(x-3)
\end{aligned}
$$

插值余项为,

$$R_3(x) = \frac{f^{(4)}(\xi_x)}{4!}x(x-1)(x-3)^2, \quad \xi_x \in [0,3]$$
$$f(2) \approx H_3(2) = \frac{83}{360} = 0.230556$$

---

#### 3. 设$f(x) = 20x^3 + 3x + 2020$, 求$f[1,2]$和$f[1,2,3,4]$. (6分)

解: $f[x_0, x_1, \cdots, x_k] = \frac{f[x_1, x_2, \cdots, x_k] - f[x_0, x_1, \cdots, x_{k-1}]}{x_k - x_0}$ (课本26页, 1.11式)

|       |          |                   |                            |                                     |
|:-----:|:--------:|:-----------------:|:--------------------------:|:-----------------------------------:|
| $x_i$ | $f(x_i)$ | $f[x_{i-1}, x_i]$ | $f[x_{i-2}, x_{i-1}, x_i]$ | $f[x_{i-3}, x_{i-2}, x_{i-1}, x_i]$ |
|   1   |   2043   |                   |                            |                                     |
|   2   |   2186   |        143        |                            |                                     |
|   3   |   2569   |        383        |             120            |                                     |
|   4   |   3312   |        743        |             180            |                  20                 |

故 $f[1,2] = 143, \quad f[1,2,3,4]=20$

另, 由于$f(x)$为三次多项式, 其三次牛顿插值多项式与$f(x)$相同, 由牛顿插值多项式的性质可知$f[1,2,3,4]$等于三次项的系数

---

#### 4. 求满足下表数据以及边界条件$S''(-2) = S''(2) = 0 \  (n=3)$的三次样条插值函数$S(x)$, 并计算$S(0)$的值. 注意: 这里的$n$为小区间个数. (6分)
|        |      |      |     |     |
|:------:|:----:|:----:|:---:|:---:|
|   $x$  | -2.0 | -1.0 | 1.0 | 2.0 |
| $f(x)$ | -4.0 |  2.0 | 5.0 | 8.0 |

解: 易知,
$$h_0 = -1.0 - (-2.0) = 1.0 \quad h_1 = 1.0 - (-1.0) = 2.0 \quad h_2 = 2.0 - 1.0 = 1.0$$

由$M$关系式 (课本42页, 1.23式), 注意到, $M_0 = S''(-2) = 0,\; M_3 = S''(2) = 0$
$$
\begin{pmatrix}
    2 & \lambda_1 \\
    \mu_2 & 2 \\
\end{pmatrix}
\begin{pmatrix}
    M_1 \\
    M_2
\end{pmatrix}
=
\begin{pmatrix}
    d_1 - \mu_1 M_0 \\
    d_2 - \lambda_2 M_3
\end{pmatrix}
=
\begin{pmatrix}
    d_1 \\
    d_2
\end{pmatrix}
$$
其中:
$$\lambda_1 = \frac{h_1}{h_0 + h_1} = \frac{2}{3} \quad
\mu_2 =  \frac{h_1}{h_1 + h_2} = \frac{2}{3}$$
$$d_1 = 6f[x_0, x_1, x_2] = \frac{6}{h_0+h_1}(\frac{f(x_2) - f(x_1)}{h_1} - \frac{f(x_1) - f(x_0)}{h_0}) = -9$$
$$d_2 = 6f[x_1, x_2, x_3] = \frac{6}{h_1+h_2}(\frac{f(x_3) - f(x_2)}{h_2} - \frac{f(x_2) - f(x_1)}{h_1}) = 3$$
$$
\Rightarrow
\begin{pmatrix}
    2 & \frac{2}{3} \\
    \frac{2}{3} & 2
\end{pmatrix}
\begin{pmatrix}
    M_1 \\
    M_2
\end{pmatrix}
=
\begin{pmatrix}
    -9 \\
    3
\end{pmatrix}
\Rightarrow
\begin{pmatrix}
    M_1 \\
    M_2
\end{pmatrix}
=
\begin{pmatrix}
    -\frac{45}{8} \\
    \frac{27}{8}
\end{pmatrix}
=
\begin{pmatrix}
    -5.625 \\
    3.375
\end{pmatrix}
$$
因此, 三次样条插值多项式为 (课本42页, 1.22式)
$$
S(x)= \left\{
\begin{aligned}
    -\frac{15}{16}&(x + 2)^3 + 4(x + 1) + \frac{47}{16}(x + 2), & x& \in [-2, -1] \\
    \frac{15}{32}&(x - 1)^3 + \frac{9}{32}(x + 1)^3 - \frac{23}{8}(x - 1) + \frac{11}{8}(x + 1), & x& \in [-1, 1] \\
    -\frac{9}{16}&(x - 2)^3 - \frac{71}{16}(x - 2) + 8(x - 1), & x& \in [1, 2] \\
\end{aligned}
\right.
$$
$$
\:\qquad=\left\{
\begin{aligned}
    -\frac{15}{16}&x^3 - \frac{45}{8}x^2 - \frac{69}{16}x + \frac{19}{8}, & x& \in [-2, -1] \\
    \frac{3}{4}&x^3 - \frac{9}{16}x^2 + \frac{3}{4}x + \frac{65}{16} & x& \in [-1, 1] \\
    -\frac{9}{16}&x^3 + \frac{27}{8}x^2 - \frac{51}{16}x + \frac{43}{8}, & x& \in [1, 2] \\
\end{aligned}
\right.
$$
$$
\:\qquad=\left\{
\begin{aligned}
    -0.9375&x^3 - 5.625x^2 - 4.3125x + 2.375, & x& \in [-2.0, -1.0] \\
    0.75&x^3 - 0.5625x^2 + 0.75x + 4.0625 & x& \in [-1.0, 1.0] \\
    -0.5625&x^3 + 3.375x^2 - 3.1875x + 5.375, & x& \in [1.0, 2.0] \\
\end{aligned}
\right.
$$
得到:
$$S(0) = \frac{65}{16} = 4.0625$$

