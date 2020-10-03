# 课后作业02

#### 1. $f(x) = \sqrt{x}$ 在离散点有$f(81) = 9$, $f(100) = 10$, $f(121) = 11$, 利用2次Lagrange插值计算$\sqrt{111}$的近似值, 并根据误差公式给出误差界. (6分)

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
    L_2(111) &= \frac{9}{760} \times 11 \times (-10) - \frac{10}{399} \times 30 \times (-10) + \frac{11}{840} \times 30 \times 11 \\
             &= \frac{2803}{266} = 10.537593985 \\
    f(111) &= \sqrt{111} = 10.535653753
\end{aligned}
$$

绝对误差: $R(x) = f(111) - L_2(111) = -0.001940232$

误差公式: $R_2(x) = \frac{f^{(3)}(\xi)}{3!}(x - 81)(x - 100)(x - 121) \qquad \xi \in [81, 121]$

误差界: $R_2(111) = -550 f^{(3)}(\xi) = -\frac{825}{4}\xi^{-\frac{5}{2}} \in [-0.003492862, -0.00128065]$

---

#### 2. 设有插值节点$a \leq x_0 < x_1 < \cdots < x_n \leq b$. 证明与这些节点相应的$Lagrange$插值基函数 $\{l_i(x), i=0,1,\cdots,n\}$ 是线性无关的。(6分)

法一: 若$l_i(x)$线性相关, 则存在不全为0的系数$a_i$, 使得
$$a_0 l_0(x) + a_1 l_1(x) + \cdots + a_n l_n(x) = 0 \qquad \forall x \in \mathbb{R} \tag{1}$$

注意到
$$l_i(x) = \frac{(x-x_0)\cdots(x-x_{i-1})(x-x_{i+1})\cdots(x-x_n)}
{(x_i-x_0)\cdots(x_i-x_{i-1})(x_i-x_{i+1})\cdots(x_i-x_n)}
=\prod_{0 \leq j \leq n, j \neq i}\frac{x-x_j}{x_i-x_j}$$

$$
l_i(x_j) = \delta_{ij} = 
    \begin{cases}
    1 & i = j \\
    0 & i \neq j
    \end{cases}
$$

将$x_i$代入(1)中, 可得
$$a_i = 0 \qquad \forall i = 0, 1, \cdots, n$$

故不存在不全为0的系数, $l_i(x)$线性无关

法二: 注意到, 若$l_i(x)$线性相关, 则线性方程组(将$x_0, x_1, \cdots, x_n$代入(1))

$$
\begin{pmatrix}
    l_0(x_0) & l_1(x_0) & \cdots & l_n(x_0) \\
    l_0(x_1) & l_1(x_1) & \cdots & l_n(x_1) \\
    \vdots   & \vdots   & \ddots & \vdots   \\
    l_0(x_n) & l_1(x_n) & \cdots & l_n(x_n)
\end{pmatrix}
\begin{pmatrix}
    a_0 \\
    a_1 \\
    \vdots \\
    a_n
\end{pmatrix}
=0
$$

有非零解, 故系数矩阵行列式为0
$$
0=
\begin{vmatrix}
    l_0(x_0) & l_1(x_0) & \cdots & l_n(x_0) \\
    l_0(x_1) & l_1(x_1) & \cdots & l_n(x_1) \\
    \vdots   & \vdots   & \ddots & \vdots   \\
    l_0(x_n) & l_1(x_n) & \cdots & l_n(x_n)
\end{vmatrix}
=
\begin{vmatrix}
    1 & 0 & \cdots & 0 \\
    0 & 1 & \cdots & 0 \\
    \vdots & \vdots & \ddots & \vdots \\
    0 & 0 & \cdots & 1
\end{vmatrix}
=1
$$
矛盾, 故$l_i(x)$线性无关

---

#### 3. 利用插值数据$(-1.0, 0.0), (1.0, 1.0), (3.0, 2.0), (4.0, -1.0)$, 并构造出三次$Lagrange$插值多项式$L_3(x)$, 并计算$L_3(0.0), L_3(2.0)$. (6分)

解:
$$
\begin{aligned}
    l_0(x) &= \ ? \quad (\text{注意到}f(x_0)=0\text{, 可以偷懒不计算}) \\
    l_1(x) &= \frac{(x + 1)(x - 3)(x - 4)}{(1 + 1)(1 - 3)(1 - 4)}
            = \frac{1}{12}(x + 1)(x - 3)(x - 4) \\
    l_2(x) &= \frac{(x + 1)(x - 1)(x - 4)}{(3 + 1)(3 - 1)(3 - 4)}
            = -\frac{1}{8}(x + 1)(x - 1)(x - 4) \\
    l_3(x) &= \frac{(x + 1)(x - 1)(x - 3)}{(4 + 1)(4 - 1)(4 - 3)}
            = \frac{1}{15}(x + 1)(x - 1)(x - 3) \\
\end{aligned}
$$
$$
\begin{aligned}
    L_3(x) &= f(x_0) l_0(x) + f(x_1) l_1(x) + f(x_2) l_2(x) + f(x_3) l_3(x) \\
           &= \frac{1}{12}(x + 1)(x - 3)(x - 4) - \frac{1}{4}(x + 1)(x - 1)(x - 4) \\
           &- \frac{1}{15}(x + 1)(x - 1)(x - 3) 
\end{aligned}
$$
$$
L_3(0.0) = -\frac{1}{5} = -0.2 \qquad L_3(2.0) = \frac{11}{5} = 2.2
$$

---

#### 4. 设$\{l_i(x)\}_{i=0}^6$是以$\{x_i=2i\}_{i=0}^6$为节点的6次Lagrange插值基函数. 试求$\sum_{i=0}^6(x_i^3 + x_i^2 + 1)l_i(x)$和$\sum_{i=0}^6(x_i^3 + x_i^2 + 1)l'_i(x)$(结果需化简). (6分)

解: 令$f(x) = x^3 + x^2 + 1$, 则

$$L_6(x) = \sum_{i=0}^6(x_i^3 + x_i^2 + 1)l_i(x) = \sum_{i=0}^6 f(x_i)l_i(x) = f(x) - R_6(x)$$

其中

$$R_6(x) = \frac{f^7(\xi)}{7!}(x-x_0)(x-x_1)\cdots(x-x_6) = 0 \quad (f^7(x) = 0, \forall x)$$

因而, $\sum_{i=0}^6(x_i^3 + x_i^2 + 1)l_i(x) = x^3 + x^2 + 1$

同时, $\sum_{i=0}^6(x_i^3 + x_i^2 + 1)l'_i(x) = (\sum_{i=0}^6(x_i^3 + x_i^2 + 1)l_i(x))' = 3x^2 + 2x$
