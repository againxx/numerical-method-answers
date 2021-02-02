# 课后作业7

#### 1. 构造积分$\bar{I}(f) = \int_{-h}^{2h}f(x)dx$的数值积分公式, $I(f) = a_{-1}f(-h) + a_0f(0) + a_1f(2h) \ (h>0)$使其具有尽可能高的代数精度, 该公式的代数精度是多少? (6分)

解: 由于数值积分公式中有三个未知数$a_{-1}, a_0, a_1$, 可假设其满足两阶代数精度, 令$f(x)$分别为$1, x, x^2$代入积分公式中

$$
\left\{
\begin{aligned}
    a_{-1} + a_0 + a_1 &= 3h = \int_{-h}^{2h}1 \cdot dx \\
    -h a_{-1} + 2h a_1 &= \frac{3}{2}h^2 = \int_{-h}^{2h}xdx \\
    h^2 a_{-1} + 4h^2 a_1 &= 3h^3 = \int_{-h}^{2h}x^2dx
\end{aligned}
\right.
$$
$$
\Rightarrow
\left\{
\begin{aligned}
    a_{-1} = 0 \\
    a_0 = \frac{9}{4}h \\
    a_1 = \frac{3}{4}h
\end{aligned}
\right.
$$

此时我们知道所求格式至少满足两阶代数精度, 但是最高的代数精度为多少?

不要忘了再将$f(x) = x^3, x^4 \cdots$代入验证, 看所得格式的代数精度为多少
$$
I(x^3) = \frac{3}{4}h \times 8h^3 = 6h^4 \neq \frac{17}{4}h^4 = \int_{-h}^{2h}x^3dx
$$
故该公式的代数精度为2

---

#### 2. 分别利用梯形公式和Simpson公式计算如下积分及其积分误差: (6分)
$$
\int_0^2 (x^3 + 5x) dx
$$

解: 梯形公式为 (课本113页, 6.1式)
$$
T(f) = \frac{b-a}{2}\lbrack f(a) + f(b) \rbrack
$$
$$
\implies T(x^3 + 5x) = \frac{2}{2} \lbrack 0 + (2^3 + 5 \times 2) \rbrack = 18
$$

由梯形公式的误差公式 (课本114页, 6.2式)
$$
E_1(f) = -\frac{f''(\eta)}{12} (b-a)^3, \ a \leq \eta \leq b
$$
$$
\implies E_1(x^3 + 5x) = -4\eta, \ 0 \leq \eta \leq 2
$$

Simpson公式为 (课本119页, 6.8式)
$$
S(f) = \frac{b-a}{6}\lbrack f(a) + 4f(\frac{a+b}{2})+ f(b) \rbrack
$$
$$
\implies S(x^3 + 5x) = \frac{2}{6} \lbrack 0 + 4 \times (1 + 5) + (2^3 + 5 \times 2) \rbrack = 14
$$

由Simpson公式的误差公式 (课本115页, 6.4式)
$$
E_2(f) = -\frac{f^{(4)}(\eta)}{2880} (b-a)^5, \ a \leq \eta \leq b
$$
$$
\implies E_2(x^3 + 5x) = 0
$$


---

#### 3. 记$I(f) = \int_{-2}^2 f(x)dx$, 设$S(f(x))$为其数值积分公式, 其中, $I(f) \approx S(f(x)) = Af(-\alpha) + Bf(0) + Cf(\alpha)$,

**a)** 试确定参数$A, B, C, \alpha$使得该数值积分公式具有尽可能高的代数精度, 并求该公式的代数精度(需给出求解过程); (5分)

**b)** 设$f(x)$足够光滑(可微). 求该数值积分公式的误差. (5分)

解: a) 法一: 将$f(x) = 1, x, x^2, x^3$分别代入原积分和数值积分公式, 得

$$
\left\{
\begin{aligned}
    A + B + C &= 4 = \int_{-2}^2 1 \cdot dx \\
    -\alpha A + \alpha C &= 0 = \int_{-2}^2 xdx \\
    \alpha^2 A + \alpha^2 C &= \frac{16}{3} = \int_{-2}^2 x^2 dx \\
    -\alpha^3 A + \alpha^3 C &= 0 = \int_{-2}^2 x^3 dx
\end{aligned}
\right.
$$

通过观察可发现, 方程$-\alpha A + \alpha C = 0$两端同时乘以$\alpha^2$,
可得方程$-\alpha^3 A + \alpha^3 C = 0$故上述线性方程组线性相关, 条件不足以解出4个未知数,
需添加$f(x) = x^4$时的方程

$$
\left\{
\begin{aligned}
    A + B + C &= 4 = \int_{-2}^2 1 \cdot dx \\
    -\alpha A + \alpha C &= 0 = \int_{-2}^2 xdx \\
    \alpha^2 A + \alpha^2 C &= \frac{16}{3} = \int_{-2}^2 x^2 dx \\
    \alpha^4 A + \alpha^4 C &= \frac{64}{5} = \int_{-2}^2 x^4 dx
\end{aligned}
\right.
$$
$$
\Rightarrow
\left\{
\begin{aligned}
    &A = \frac{10}{9} \\
    &B = \frac{16}{9} \\
    &C = \frac{10}{9} \\
    &\alpha = \pm \sqrt{\frac{12}{5}}
\end{aligned}
\right.
$$

为进一步确定代数精度, 将$f(x) = x^5, x^6, \cdots$代入积分公式
$$
\begin{aligned}
    -\alpha^5 A + \alpha^5 C &= 0 = \int_{-2}^2 x^5dx \\
    \alpha^6 A + \alpha^6 C &= \frac{768}{25} \neq \frac{256}{7} = \int_{-2}^2 x^6 dx
\end{aligned}
$$
可知该积分格式的代数精度为5阶

---

法二: 注意观察可知, 该积分公式的积分区间对称, 且三点Gauss-Legendre积分公式包含零点,
故可直接查询书上131页的表6.4得到
$$
\begin{aligned}
    \alpha &= \frac{(a + b) + (b - a) x_1^{(3)}}{2} = 2x_1^{(3)} = 1.549193 \\
    A &= \frac{(b-a)}{2} \alpha_1^{(3)} = 2 \alpha_1^{(3)} = 1.111111 \\
    B &= \frac{(b-a)}{2} \alpha_2^{(3)} = 2 \alpha_2^{(3)} = 1.777778 \\
    C &= \frac{(b-a)}{2} \alpha_3^{(3)} = 2 \alpha_3^{(3)} = 1.111111
\end{aligned}
$$
代数精度应为$2n - 1 = 5$阶

b) Gauss积分误差为 (PPT ch62_4, 50页)
$$
\begin{aligned}
    E_n(f) &= I(f) - S(f) = \frac{f^{(2n)}(\xi)}{(2n)!} \int_a^b W(x) \omega_n^2 (x) dx \\
           &= \frac{f^{(6)}(\xi)}{6!} \int_{-2}^2 (x - \alpha)^2 x^2 (x + \alpha)^2 dx \\
           &= \frac{f^{(6)}(\xi)}{6!} \int_{-2}^2 (x^2 - \alpha^2)^2 x^2 dx \\
           &= \frac{f^{(6)}(\xi)}{6!} \int_{-2}^2 (x^2 - \frac{12}{5})^2 x^2 dx \\
           &= \frac{f^{(6)}(\xi)}{6!} \int_{-2}^2 x^6 - \frac{24}{5}x^4 + \frac{144}{25}x^2 dx \\
           &= \frac{f^{(6)}(\xi)}{6!} \frac{1024}{175} = \frac{64}{7875} f^{(6)}(\xi), \  \xi \in [-2, 2]
\end{aligned}
$$
