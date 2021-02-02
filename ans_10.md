# 课后作业10

#### 1. 试推导例题7.4 (第3版教材151-152页)中的差分格式的局部截断误差, (10分)
$$ y_{n+1} = y_{n-1} + \frac{h}{3} [7f(x_n, y_n) - 2f(x_{n-1}, y_{n-1}) + f(x_{n-2}, y_{n-2})] $$
即验证
$$ T_{n+1} \equiv y(x_{n+1}) - y_{n+1} = \frac{1}{3} h^4 y^{(4)}(x_{n-1}) + O(h^5) $$
(提示: 将差分格式右端的某些项在某点处同时作Taylor展开)

解: 计算局部截断误差时,
* 假设之前的计算都是精确的, 即$y_{n-1} = y(x_{n-1})$
* 观察差分格式两端, 选择公共项最多的节点展开 (这里选择$x_{n-1}$)

各项Taylor展开的结果为,
$$
\begin{aligned}
    &f(x_n, y_n) = y'(x_n) \\
    &= y'(x_{n-1}) + hy''(x_{n-1}) + \frac{1}{2}h^2y^{(3)}(x_{n-1}) + \frac{1}{6}h^3y^{(4)}(x_{n-1}) + \frac{1}{24}h^4y^{(5)}(x_{n-1}) \\
    &+ O(h^5)
\end{aligned}
$$

$$ f(x_{n-1}, y_{n-1}) = y'(x_{n-1}) $$

$$
\begin{aligned}
    &f(x_{n-2}, y_{n-2}) = y'(x_{n-2}) \\
    &= y'(x_{n-1}) - hy''(x_{n-1}) + \frac{1}{2}h^2 y^{(3)}(x_{n-1}) - \frac{1}{6}h^3 y^{(4)}(x_{n-1}) + \frac{1}{24}h^4 y^{(5)}(x_{n-1}) \\
    &+ O(h^5)
\end{aligned}
$$

$$
\begin{aligned}
    &y(x_{n+1}) \\
    &= y(x_{n-1}) + 2h y'(x_{n-1}) + 2h^2 y''(x_{n-1}) + \frac{4}{3}h^3 y^{(3)}(x_{n-1}) + \frac{2}{3}h^4 y^{(4)}(x_{n-1}) \\
    &+ \frac{4}{15}h^5y^{(5)} + O(h^6)
\end{aligned}
$$

根据Taylor展开结果制成如下表格

![ans_10_table](https://gitee.com/againxx/image-storage/raw/master/images/20200530185936.png =750x)

通过表格最后一项可看出
$$ T_{n+1} \equiv y(x_{n+1}) - y_{n+1} = \frac{1}{3} h^4 y^{(4)}(x_{n-1}) + O(h^5) $$

#### 2. 试用线性多步法构造$p=1, q=2$时的隐式差分格式, 求该格式局部截断误差的误差主项并判断它的阶(即精度), 最后为该隐式格式设计一种合适的预估-校正格式. (10+1+4=15分)

解: $p=1 \implies$积分区间为$[x_{n-1}, x_{n+1}]$

$\ \quad q=2$ 的隐格式$\implies$积分节点为$\{x_{n+1}, x_n, x_{n-1}\}$

故有差分格式:
$$ y_{n+1} = y_{n-1} + [\alpha_0 f(x_{n+1}, y_{n+1}) + \alpha_1 f(x_n, y_n) + \alpha_2 f(x_{n-1}, y_{n-1})] $$

下一步, 根据$\alpha_j = \int_{x_{n-1}}^{x_{n+1}} l_j(x)dx$确定积分系数, 这里可作变换$y=x-x_n$来简化计算
$$
\begin{aligned}
    \alpha_0 &= \int_{x_{n-1}}^{x_{n+1}} \frac{(x-x_n)(x-x_{n-1})}{(x_{n+1}-x_n)(x_{n+1}-x_{n-1})}dx
              = \frac{1}{2h^2} \int_{-h}^h y(y+h)dy = \frac{1}{3}h \\
    \alpha_1 &= \int_{x_{n-1}}^{x_{n+1}} \frac{(x-x_{n+1})(x-x_{n-1})}{(x_n-x_{n+1})(x_n-x_{n-1})}dx
              = -\frac{1}{h^2} \int_{-h}^h (y-h)(y+h)dy = \frac{4}{3}h \\
    \alpha_2 &= \int_{x_{n-1}}^{x_{n+1}} \frac{(x-x_{n+1})(x-x_n)}{(x_{n-1}-x_{n+1})(x_{n-1}-x_n)}dx
              = \frac{1}{2h^2} \int_{-h}^h (y-h)ydy = \frac{1}{3}h
\end{aligned}
$$

从而得到差分格式,
$$ y_{n+1} = y_{n-1} + h[\frac{1}{3} f(x_{n+1}, y_{n+1}) + \frac{4}{3} f(x_n, y_n) + \frac{1}{3} f(x_{n-1}, y_{n-1})] $$

下一步求所得格式的局部截断误差, 将右端各项均在$x_{n-1}$处Taylor展开

$$ y_{n-1} = y(x_{n-1}) $$

$$ f(x_{n-1}, y_{n-1}) = y'(x_{n-1}) $$

$$
\begin{aligned}
    &f(x_n, y_n) = y'(x_n) \\
    &= y'(x_{n-1}) + hy''(x_{n-1}) + \frac{1}{2}h^2 y^{(3)}(x_{n-1}) + \frac{1}{6}h^3 y^{(4)}(x_{n-1}) + \frac{1}{24}h^4 y^{(5)}(x_{n-1}) \\
    &+ O(h^5)
\end{aligned}
$$

注意对于节点$x_{n+1}$我们无法假设计算是精确的, 故$y_{n+1} \neq y(x_{n+1})$,

因而$f(x_{n+1}, y_{n+1}) \neq f(x_{n+1}, y(x_{n+1})) = y'(x_{n+1})$

为了计算$f(x_{n+1}, y_{n+1})$在$x_{n-1}$处的Taylor展开, 我们先计算$f(x_{n+1}, y(x_{n+1}))$在$x_{n-1}$处的Taylor展开,
再计算$f(x_{n+1}, y_{n+1})$与$f(x_{n+1}, y(x_{n+1}))$的关系

$$
\begin{aligned}
    &f(x_{n+1}, y(x_{n+1})) = y'(x_{n+1}) \\
    &= y'(x_{n-1}) + 2hy''(x_{n-1}) + 2h^2 y^{(3)}(x_{n-1}) + \frac{4}{3}h^3 y^{(4)}(x_{n-1}) + \frac{2}{3}h^4 y^{(5)}(x_{n-1}) \\
    &+ O(h^5)
\end{aligned}
$$

随后, 记 $T_{n+1} = y(x_{n+1}) - y_{n+1}$
$$ f(x_{n+1}, y_{n+1}) = f(x_{n+1}, y(x_{n+1}) - T_{n+1}) = f(x_{n+1}, y(x_{n+1})) - T_{n+1}f_y(x_{n+1}, \xi) $$

对$y(x_{n+1})$进行Taylor展开
$$
\begin{aligned}
    y(x_{n+1}) &= y(x_{n-1}) + 2hy'(x_{n-1}) + 2h^2 y''(x_{n-1}) + \frac{4}{3}h^3 y^{(3)}(x_{n-1}) + \frac{2}{3}h^4 y^{(4)}(x_{n-1}) \\
               &+ \frac{4}{15}h^5 y^{(5)}(x_{n-1}) + O(h^6)
\end{aligned}
$$

通过合并Taylor展开的各项, 局部截断误差为
$$ T_{n+1} = y(x_{n+1}) - y_{n+1} = -\frac{1}{90}h^5 y^{(5)}(x_{n-1}) + \frac{h}{3} T_{n+1} f_y(x_{n+1}, \xi) + O(h^6) $$
$$
\begin{aligned}
    \implies T_{n+1} &= \frac{-\frac{1}{90}h^5 y^{(5)}(x_{n-1}) + O(h^6)}{1 - \frac{h}{3}f_y(x_{n+1}, \xi)} \\
                     &= (-\frac{1}{90}h^5 y^{(5)}(x_{n-1}) + O(h^6))(1 + \frac{h}{3}f_y(x_{n+1}, \xi) + \cdots ) \\
                     &= (\underbrace{-\frac{1}{90}h^5 y^{(5)}(x_{n-1})}_{误差主项} + O(h^6))
\end{aligned}
$$

该格式局部截断误差为$O(h^5)\rightarrow$ 具有4阶精度
* 起步计算时, 为了不影响格式的整体截断误差, 应使用不少于 **三阶** 的格式(课本152页)
* 预估-校正时尽量使用 **四阶** 的显格式作为预估步的计算

可使用四阶Runge-Kutta公式
$$
\left\{
\begin{aligned}
    \bar{y}_{n+1} &= y_n + \frac{h}{6} (k_1 + 2k_2 + 2k_3 + k_4) \\
                  &k_1 = f(x_n, y_n)  \\
                  &k_2 = f(x_n + \frac{1}{2}h, y_n + \frac{1}{2}h k_1) \\
                  &k_3 = f(x_n + \frac{1}{2}h, y_n + \frac{1}{2}hk_2) \\
                  &k_4 = f(x_n + h, y_n + hk_3) \\
    y_{n+1} &= y_{n-1} + h[\frac{1}{3} f(x_{n+1}, \bar{y}_{n+1}) + \frac{4}{3}f(x_n, y_n) + \frac{1}{3}f(x_{n-1}, y_{n-1})]
\end{aligned}
\right.
$$
