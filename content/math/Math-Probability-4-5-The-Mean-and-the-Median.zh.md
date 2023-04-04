---
title: 【概率论】4-5:均值和中值(The Mean and the Median)
categories:
    - Mathematic
    - Probability
tags:
    - 均值
    - 中值
    - 最小均值误差
    - 最小绝对误差
toc: true
date: 2018-03-25 21:01:04
---

**Abstract:** 本文介绍均值和中值的对比，以及最小平方误差，最小绝对误差
**Keywords:** Mean，Median，Mean Squared Error，Mean Absolute Error

<!--more-->
# 均值和中值
昨天犯了个大错误，google分析配置出错了，所以这两天博客访问一直显示零，所以昨天都很沮丧，生活有时候就这样，一些错误，后果非常让人非常沮丧，我们在面对这些沮丧的结果时的态度能决定我们的所有。
均值是度量分布中心位置的一种方法，中值也是，这就是我们上一篇说到的，关于一个属性的定义，我们现在定义分布的中心位置，就有了两种方法，这两种都能定义中心的合理方法，各有各的优点，也有自己的缺点，所以我们今天就来对比下这两种中心位置的数字特点。
## 中位数 The Median
4.1中介绍过一个分布的的期望，是在随机变量所在的数轴的重心位置，这种角度下，期望是一个中心位置。
另一种就是假设存在某个随机变量 $m_0$ 小于 $m_0$ 对应的概率是 $1/2$ 大于 $m_0$ 的对应概率为 $1/2$ 这从某种意义上说也是一个中心位置。
两个不一样的定义方式，就有两种不同的方法用于不同的问题
最简单的例子就是图像处理里面两种不同的滤波，均值滤波和中值滤波，对应处理的噪声也完全不同。
均值，也就是期望我们已经研究了4篇了，今天我们主要研究一下中值，虽然在c.d.f中有介绍，但是我们还是重新说说。
值得一提的是与均值不同，分布的均值可以有一个或者没有，而中值可以有一个，还可以有很多个，这个我们后面会说到。

>Definition Median.Let $X$ be a random varibale.Every number $m$ with the following prperty is called a median of the distribution of $X$:
$$
\begin{aligned}
Pr(X\leq m)\geq 1/2\
\end{aligned}
\text{ and  }
\begin{aligned}
Pr(X\geq m)\geq 1/2
\end{aligned}
$$

中值的定义如上，还有一种跟奇特的说法和上面是等价的。

> Firest,if m is included with the values of X to the left of m,then
$$
Pr(X\leq m)\geq Pr(X>m)
$$

>seconde ,if m is included with the values of X to the right of m,then
$$
Pr(X\geq m)\geq Pr(X<m)
$$

>If there is a number $m$ such that $Pr(X <  m)=Pr(X > m)$ ,that is,if the number $m$ does actually divide the total Probability into two equal parts,then $m$ will of course be a median of the distribution of $X$

两种定义中值的方法得到一样的结果。值得注意的就是一点，中值可能不止一个，当中值不止一个的时候我们这里选用最小的作为中值，当然，也可以选中间的，或者最大的，这取决于你自己的需求。

文章写到这里，书上开始写🌰，目测有一斤🌰 。例子的核心就是中值不一定只有一个。
## 均值和中值的比较 Comparison of the Mean and the median
最重要的一个区别就是期望有些分布是没有的，但是中值绝对存在，而且有很多时候还不止一个。所以对于某些应用中值的稳定性更好，最简单的例子就是我们伟大祖国各个城市的平均收入贼高，但是你和周围的小伙伴总发现自己拖后腿，那么这时候平均值可能真的不能反映实际的情况，需要用中值，如果你的工资连中值都没到，说明你确实不行，你说你比不过马云马化腾我们理解，你连你隔壁都不如，那就是你的问题了。
下面定义一个双射函数，这个证明我不写了，书上有，但是我觉得不完美，因为我马上要在数学分析那个系列里面讲这个情况，所以这里只给出定理，着急的小伙伴就自己查查资料，不着急的，等我数学分析。

>Theorem One-to-One Function.Let $X$ be a random variable that takes values in an interval $I$ of real numbers.Let $r$ be a one-to-one function defined on the interval $I$.If $m$ is a median of $X$ ,then $r(m)$ is a median of $r(X)$

其实用到的主要特性是双射函数的可逆性质，换句话说就是能找到反函数。

接下来我们开始进入到很贴近应用的部分了。
## 最小均方误差 Minimizing the Mean Squared Error
假设某随机变量 $X$ 其期望是 $\mu$ 方差是 $\sigma^2$ ，并且假设，$X$ 是通过某种试验得到的结果，现在我们还没有做实验，但是我们希望预测下结果，应该怎么做。
这个课题熟悉不？买彩票，买股票，赌博，各位老铁，激动了么，说实话，想指着学了这点概率发家致富，你还是去睡觉吧，可能睡觉致富更快一点。
为了预测出一个靠谱的结果，我们要做的第一件事不是找结果，而是告诉大家啥样的猜测算靠谱。你总预测我能当美国总统也不现实。
靠谱，就是错误小，没法生的时候，就是发生错误的可能性小，换句话说，就是犯错的期望值最小。

>Definition Mean Squared Error/M.S.E.. The number $E[(X-d)^2]$ is called the mean squared error(M.S.E) of prediction $d$ .

这个地方定义了错误，也就是什么是不靠谱的概率，也就是靠谱的概率。

>Theorem Let $X$ be a random varibale with finite variance $\sigma^2$ ,and let $\mu=E(X)$ .For every number $d$ ,
$$
E[(X-\mu)^2]\leq E[(X-d)^2]
$$
Furthermore ,there will be equality in the relation if and only if $d=\mu$

上面这个定理是说任何随机变量的均方误差都是大于等于方差的，等于号当且仅当d是均值的时候成立，我们需要证明下：
$$
\begin{aligned}
E[(X-d)^2]&=E(X^2+2dX+d^2)\\
&=E(X^2)-2d\mu+d^2
\end{aligned}
$$

上面式子中，只有当 $d=\mu$ 的时候才能得到最小值，这个最小值也就是方差，简单的求最值，这里就不啰嗦了。

所以在一个分布已知的情况下，预测就预测均值，其均方误差一定是最小的。

## 最小化绝对误差均值 Minimizing the Mean Absolute Error
跟上面的最小均方误差出发点类似的，也是我们先要定义一个误差，这个误差越大表示结果越不好，那么：

>Definition Mean Absolute Error/M.A.E. The number $E(|X-d|)$ is called the mean absolute error (M.A.E) of the prediction $d$ .

接下来我们要看到的是，在这种误差定义下，我们得到的最优猜测是中值，而不是均值。

>Theorem Let $X$ be a random variable with finite mean,and let $m$ be a median of the distribution of $X$ .For every number $d$ ,
$$
E(|X-m|)\leq E(|X-d|)
$$
Furthermore,there will be equality in the relation if and only if $d$ is also a median of the distribution of $X$


上面定义的绝对误差期望 M.A.E.在最小化时得到的最优猜测是中值，我们必须要证明一下。
证明：
我们假设连续随机变量 $X$ 的p.d.f.是 $f$ 所有不同的分布都是类似的。
首先假设 $d > m$ 其中 $m$ 是中值

$$
E(|X-d|)-E(|X-m|)=\int^{\infty}_{-\infty}(|x-d|-|x-m|)f(x)dx\\
=\int^{m}_{-\infty}(d-m)f(x)dx+\int^{d}_{m}(d+m-2x)fxdx+\int^{\infty}_{d}(m-d)f(x)dx\\
\geq \int^{m}_{-\infty}(d-m)f(x)dx+\int^{d}_{m}(d+m)fxdx+\int^{\infty}_{d}(m-d)f(x)dx\\
=(d-m)[Pr(X\leq m)-Pr(X > m)]
$$

因为 $d > m$  且 $m$ 是中值,那么：
$$
Pr(X\leq m)\geq 1/2 \geq Pr(X>m)
$$
所以上的结果必然是个非负数，最小值只能是当 $d=m$ 时候才相等，因此 $E(|X-d|)\geq E(|X-m|)$.

同理可以证明 $d < m$ 时候的情况。

## 关于M.S.E. 和M.S.A. 是否有限的重要结论
观察 M.S.E和M.A.E我们发现，每个分布都有中值，但是这两个误差是否有限其实和中值无关，从定义上看，只有随机变量的方差存在的时候，M.S.E才有限，只有当分布的期望存在时， M.A.E 才有限。

## 总结
对标均值和中值，得到一些重要的结论，尤其是后面有关于预测的部分，这个是机器学习里面比较常用到的基础知识，大家要好好掌握！
待续。。。





