# 课后作业10

#### 1. 试推导例题7.4 (第3版教材151-152页)中的差分格式的局部截断误差, (10分)
$$ y_{n+1} = y_{n-1} + \frac{h}{3} [7f(x_n, y_n) - 2f(x_{n-1}, y_{n-1}) + f(x_{n-2}, y_{n-2})] $$
即验证
$$ T_{n+1} \equiv y(x_{n+1}) - y_{n+1} = \frac{1}{3} h^4 y^{4}(x_{n-1}) + O(h^5) $$
(提示: 将差分格式右端的某些项在某点处同时作Taylor展开)

#### 2. 试用线性多步法构造$p=1, q=2$时的隐式差分格式, 求该格式局部截断误差的误差主项并判断它的阶(即精度), 最后为该隐式格式设计一种合适的预估-校正格式. (10+1+4=15分)