# 课后作业01

#### 1. 阅读绪论并给出计算如下函数的可靠数值计算方法，使其尽量达到更好的精度 (6分)

(1). $f(x) = (a+x)^n - a^n$  
(2). $f(x) = cos(a - x) - cos(a)$  
(3). $f(x) = x - \sqrt{(x^2 + a)}$

其中, n为正整数, __(1)__ __(2)__ 中的$x$很靠近0且$a>0$, __(3)__ 中$x>>a$

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
f(x) = cos&(a - x) - cos(a) \\
     = cos&(a - \frac{x}{2} - \frac{x}{2})
     - cos(a - \frac{x}{2} + \frac{x}{2}) \\
     \overset{和角公式}{=} cos&(a - \frac{x}{2})cos(\frac{x}{2})
     + sin(a - \frac{x}{2})sin(\frac{x}{2})
     - cos(a - \frac{x}{2})cos(\frac{x}{2}) \\
     + sin&(a - \frac{x}{2})sin(\frac{x}{2}) \\
     = 2sin&(a - \frac{x}{2})sin(\frac{x}{2})
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

#### 2. 设有精确值$x^*=2021.3005$, 其近似值$x=2021.3000$有几位有效数字? 近似值$x$的绝对误差是多少? (2分)

解: 绝对误差 $e = x^* - x = 5 \times 10^{-4}\qquad$
绝对误差限 $|e| = 5 \times 10^{-4} \leq \frac{1}{2} \times 10^{-3}$

有效位数从小数点后第三位开始算, $x = \underbrace{2021.300}_\text{7位有效数字}0$

