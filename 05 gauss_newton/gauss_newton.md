
[commit]:<> (作者：涂啥)
[commit]:<> (邮箱：1343163818@qq.com)
[commit]:<> (开始时间：2022.03.20)
[commit]:<> (完成时间：)


# <center>高斯牛顿迭代法</center>
## 背景  
高斯牛顿迭代法是为了解决非线性最小二乘问题。为什么只能适用于非线性最小二乘呢？在高斯牛顿之前非线性最小二乘使用的是什么算法呢？

## 问题建模
高斯牛顿迭代法解决的是如下的非线性最小二乘问题
$$
    x = \mathop {arg\min} \limits_{x}\frac{1}{2}\left\| f\left( x \right) \right\| ^2 \tag{1}
$$
$f(x)$在$x=x_0$处的一阶泰勒展开式为
$$
    f(x) = f(x_0) + f^{'}(x_0)(x-x_0)+o(x-x_0) \tag{2}
$$
所以$f(x_k+\varDelta x)$在$x_k$处的泰勒展开式为
$$
\begin{aligned}
    f(x_k + \varDelta x)&=f(x_k)+f^{'}(x_k)\varDelta x + o(\varDelta x)  \\
    &=f(x_k)+J(x_k)\varDelta x + o(\varDelta x)\tag{3}
\end{aligned}
$$

$$
\begin{aligned}
\frac{1}{2}\left\| f\left( x_k+\varDelta x \right) \right\| ^2&=\frac{1}{2}f\left( x+\varDelta x \right) ^Tf\left( x+\varDelta x \right) \\
&\approx \frac{1}{2}\left[ f\left( x_k \right) +J\left( x_k \right) \varDelta x \right] ^T\left[ f\left( x_k \right) +J\left( x_k \right) \varDelta x \right] \\
&=\frac{1}{2}\left[ f\left( x_k \right) ^Tf\left( x_k \right) +f\left( x_k \right) ^TJ\left( x_k \right) \varDelta x+\varDelta x^TJ\left( x_k \right) ^Tf\left( x_k \right) +\varDelta x^TJ\left( x_k \right) ^TJ\left( x_k \right) \varDelta x \right] \\
&=\frac{1}{2}\left[ f\left( x_k \right) ^Tf\left( x_k \right) +2f\left( x_k \right) ^TJ\left( x_k \right) \varDelta x+\varDelta x^TJ\left( x_k \right) ^TJ\left( x_k \right) \varDelta x \right] 
\tag{4}
\end{aligned}
$$
首先对公式（4）做一个简要的解释：由公式（3）可知，假设$\varDelta x$为$n*1$维矩阵，所以$f$也为$n*1$,又因为范数为"距离的量测"为一标量，所以展开后就为$f^Tf$。同理$f\left( x_k \right) ^TJ\left( x_k \right) \varDelta x$ 与 $\varDelta x^TJ\left( x_k \right) ^Tf\left( x_k \right)$最终都为一标量，参与计算的参数一致，结果一致，因此就合并计算了。  
若$\frac{1}{2}\left\| f\left( x_k+\varDelta x \right) \right\| ^2$在某一点处最小则有一阶导数在该处为0，即
$$
\frac{\partial \frac{1}{2}\left\| f\left( X_k+\varDelta x \right) \right\| ^2}{\partial \varDelta x} = J(x_k)^TJ(x_k)\varDelta x +J(x_k)^Tf(x_k) = 0。 \tag{5}

$$
所以可以得到，
$$
\varDelta x = -( J(x_k)^TJ(x_k))^{-1}J(x_k)^Tf(x_k)。 \tag{6}
$$
最终的高斯牛顿迭代公式为
$$
    x_{k+1} = x_{k} - ( J(x_k)^TJ(x_k))^{-1}J(x_k)^Tf(x_k)。 \tag{7}
$$
