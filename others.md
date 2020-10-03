# 其余习题

#### 对常微分方程$\left\{ \begin{smallmatrix} y' = f(x,y) \\ y(a) = b \end{smallmatrix} \right.$, 在等距节点下构造如下的线性多步格式
$$
y_{n+1} + (\alpha - 1)y_n - \alpha y_{n-1} = \frac{h}{4} [(\alpha + 3)f_{n+1} + (3\alpha + 1)f_{n-1}]
$$
假设节点间距为$h$

1. 证明$\alpha \neq -1$时格式是二阶精度的(即格式的局部截断误差为$O(h^3)$), 当$\alpha = -1$时格式是三阶精度的.
2. 当$\alpha = -1$时, 说明格式是几步几阶显式还是隐式格式.

解: 将右端各项均在$x_{n-1}$处Taylor展开

$$ y_{n-1} = y(x_{n-1}) $$

$$
\begin{aligned}
    y_n = y(x_n) &= y(x_{n-1}) + hy'(x_{n-1}) + \frac{h^2}{2}y''(x_{n-1}) + \frac{h^3}{6}y^{(3)}(x_{n-1}) + \frac{h^4}{24}y^{(4)}(x_{n-1}) \\
    &+ O(h^5)
\end{aligned}
$$
$$ f(x_{n-1}, y_{n-1}) = y'(x_{n-1}) $$

注意对于节点$x_{n+1}$我们无法假设计算是精确的, 故$y_{n+1} \neq y(x_{n+1})$,

因而$f(x_{n+1}, y_{n+1}) \neq f(x_{n+1}, y(x_{n+1})) = y'(x_{n+1})$

为了计算$f(x_{n+1}, y_{n+1})$在$x_{n-1}$处的Taylor展开, 我们先计算$f(x_{n+1}, y(x_{n+1}))$在$x_{n-1}$处的Taylor展开,
再计算$f(x_{n+1}, y_{n+1})$与$f(x_{n+1}, y(x_{n+1}))$的关系

$$
\begin{aligned}
    &f(x_{n+1}, y(x_{n+1})) = y'(x_{n+1}) \\
    &= y'(x_{n-1}) + 2hy''(x_{n-1}) + 2h^2 y^{(3)}(x_{n-1}) + \frac{4}{3}h^3 y^{(4)}(x_{n-1}) + O(h^4)
\end{aligned}
$$

随后, 记 $T_{n+1} = y(x_{n+1}) - y_{n+1}$
$$ f(x_{n+1}, y_{n+1}) = f(x_{n+1}, y(x_{n+1}) - T_{n+1}) = f(x_{n+1}, y(x_{n+1})) - T_{n+1}f_y(x_{n+1}, \xi) $$

对$y(x_{n+1})$进行Taylor展开
$$
\begin{aligned}
    y(x_{n+1}) &= y(x_{n-1}) + 2hy'(x_{n-1}) + 2h^2 y''(x_{n-1}) + \frac{4}{3}h^3 y^{(3)}(x_{n-1}) + \frac{2}{3}h^4 y^{(4)}(x_{n-1}) \\
               &+ O(h^5)
\end{aligned}
$$

通过合并Taylor展开的各项, 局部截断误差为
$$
\begin{aligned}
T_{n+1} &= y(x_{n+1}) - y_{n+1} = \frac{\alpha + 1}{3}h^3 y^{(3)}(x_{n-1}) + \frac{7 \alpha + 9}{24}h^4 y^{(4)}(x_{n-1}) \\
           &+ \frac{h(\alpha + 3)}{4} T_{n+1} f_y(x_{n+1}, \xi) + O(h^5)
\end{aligned}
$$

可知当$\alpha = -1$时, 为3阶精度, 此时格式为
$$
y_{n+1} = 2y_n - y_{n-1} + \frac{h}{4} [2f_{n+1} - 2f_{n-1}]
$$

**三步三阶隐格式**
