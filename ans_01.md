# 课后作业01

#### 1. 阅读绪论并给出计算如下函数的可靠数值计算方法，使其尽量达到更好的精度 (10分=4+3+3)

(1). $f(x) = (a+x)^n - a^n$  
(2). $f(x) = cos(a + x) - cos(a)$  
(3). $f(x) = x - \sqrt{(x^2 + a)}$

其中, __(1)__ __(2)__ 中的$x$很靠近0且$a>0$, __(3)__ 中$x>>a$

第(1)题
$$\begin{aligned}
f(x) &= (a+x)^n - a^n \\
     &= C_n^0 a^n + C_n^1 a^{n-1}x + \cdots + C_n^n x^n - a^n \\
     &= C_n^1 a^{n-1}x + C_n^2 a^{n-2}x^2 + \cdots + C_n^n x^n
\end{aligned}\tag{1.1}$$

或
$$\begin{aligned}
f(x) &= (a+x)^n - a^n \\
     &= (a+x - a)((a+x)^{n-1} + a(a+x)^{n-2} + \cdots + a^{n-1}) \\
     &= x((a+x)^{n-1} + a(a+x)^{n-2} + \cdots + a^{n-1})
\end{aligned}\tag{1.2}$$

第(2)题
$$\begin{aligned}
f(x) = cos&(a + x) - cos(a) \\
     = cos&(a + \frac{x}{2} + \frac{x}{2})
     - cos(a + \frac{x}{2} - \frac{x}{2}) \\
     \overset{和角公式}{=} cos&(a + \frac{x}{2})cos(\frac{x}{2})
     - sin(a + \frac{x}{2})sin(\frac{x}{2})
     - cos(a + \frac{x}{2})cos(\frac{x}{2}) \\
     - sin&(a + \frac{x}{2})sin(\frac{x}{2}) \\
     = -2sin&(a + \frac{x}{2})sin(\frac{x}{2})
\end{aligned}\tag{2}$$

第(3)题
$$\begin{aligned}
f(x) &= x - \sqrt{(x^2 + a)} \\
     &= \frac{(x - \sqrt{(x^2 + a)})(x + \sqrt{(x^2 + a)})}
     {x + \sqrt{(x^2 + a)}} \\
     &= \frac{x^2 - (x^2 + a)}
     {x + \sqrt{(x^2 + a)}} \\
     &= \frac{-a}
     {x + \sqrt{(x^2 + a)}}
\end{aligned}\tag{3}$$

需避免:
* __两相近数相减__ -> __相对误差增大__ (1, 2, 3题均属于这种情况)
* __小数作除数__ -> __绝对误差增大__

---

#### 2. 设有精确值$x^*=0.0202005$, 则其近似值$x=0.020200$有几位有效数字? 近似值$x$的绝对误差是多少? (5分)

解: 绝对误差 $e = x^* - x = 5 \times 10^{-7}\qquad$
绝对误差限 $|e| = 5 \times 10^{-7} \leq \frac{1}{2} \times 10^{-6}$

有效位数从小数点后第六位开始算, $x = 0.0\underbrace{20200}_\text{5位有效数字}$

---

#### 3. 设有插值节点$a \leq x_0 < x_1 < \cdots < x_n \leq b$. 证明与这些节点相应的$Lagrange$插值基函数 $\{l_i(x), i=0,1,\cdots,n\}$ 是线性无关的。(5分)

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

#### 4. 利用插值数据$(-1.0, 0.0), (1.0, 1.0), (4.0, 2.0), (5.0, 4.0)$, 并构造出三次$Lagrange$插值多项式$L_3(x)$, 并计算$L_3(2.0), L_3(4.0)$. (10分)

解:
$$
\begin{aligned}
    l_0(x) &= \ ? \quad (\text{注意到}f(x_0)=0\text{, 可以偷懒不计算}) \\
    l_1(x) &= \frac{(x + 1)(x - 4)(x - 5)}{(1 + 1)(1 - 4)(1 - 5)}
            = \frac{1}{24}(x + 1)(x - 4)(x - 5) \\
    l_2(x) &= \frac{(x + 1)(x - 1)(x - 5)}{(4 + 1)(4 - 1)(4 - 5)}
            = -\frac{1}{15}(x + 1)(x - 1)(x - 5) \\
    l_3(x) &= \frac{(x + 1)(x - 1)(x - 4)}{(5 + 1)(5 - 1)(5 - 4)}
            = \frac{1}{24}(x + 1)(x - 1)(x - 4) \\
\end{aligned}
$$
$$
\begin{aligned}
    L_3(x) &= f(x_0) l_0(x) + f(x_1) l_1(x) + f(x_2) l_2(x) + f(x_3) l_3(x) \\
           &= \frac{1}{24}(x + 1)(x - 4)(x - 5) - \frac{2}{15}(x + 1)(x - 1)(x - 5) \\
           &+ \frac{1}{6}(x + 1)(x - 1)(x - 4) 
\end{aligned}
$$
$$
L_3(2.0) = \frac{19}{20} = 0.95 \qquad L_3(4.0) = 2.0 \ (\text{由插值性直接得出})
$$
