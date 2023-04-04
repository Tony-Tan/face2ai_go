---
title: 【概率论】3-6:条件分布(Conditional Distributions Part I）
categories:
  - Mathematic
  - Probability
tags:
  - 离散条件分布
  - 连续条件分布

toc: true
date: 2018-03-08 10:38:13
---

**Abstract:** 首先介绍随机变量的条件分布，随后介绍随机变量条件分布下的乘法法则，贝叶斯公式和全概率公式
**Keywords:** Discrete Conditional Distributions，Continuous Conditional Distributions，Multiplication Rule，Bayes' Therom，Law of Total Probability

<!--more-->
# 条件分布
隔了半个月没有研究数学，早上起来还激动不已，看了两页书好几脸懵x
> “如何变成一个真正的行家”
- 花几年时间进行紧张的学习，直到你觉得自己在行
- 离开几年，去探索更多其他的领域，无论是否有关
- 回到原来的领域，换个角度，重新掌握它
也许这与传统观点相悖，但你可以不用练习就升级，有时候这是升级的唯一办法

上面这段话引自Francois Chollet

这段话不适合小菜，只适合大牛们冲击天花板，我们小菜现在要做的就是第一步，花几年时间进行紧张的学习。
简短的回顾下前面的内容，我们从试验出发，然后得到事件，从事件引出对应的概率，然后把事件数字化后，随机变量作为一个函数成为我们研究的对象，在研究事件的时候我们研究了形如 $Pr(A|B)$ 的事件的条件概率，并且把它用到了全概率公式，贝叶斯公式等，并了解到其性质和普通事件的概率一致，甚至所有事件都可以定义为条件事件，条件概率从一开始就注定成为我们研究的重要一部分，所以当事件数字化之后，条件分布也就成了研究的重点，没错，我们今天这一大篇都是研究条件分布的，目前之研究两个随机变量的条件分布，多变量的可以依靠两个变量的推导出来。
在联合分布中的条件分布，上一篇的边缘分布也是我们要使用到的，所以上一篇的内容需要大家详细掌握。
## 离散条件分布 Discrete Conditional Distributions
上来先举个🌰 ：
保险公司想要研究哪种型号的车更容易被盗，研究出了下面这个表的数据：
![](./car.png)
表中1表示被盗，0表示没有被盗，Y表示车型，保险公司会根据不同的车型设定保险金（奸商都特别会算账，不然会赔到死），如果我们不知道你是什么车，从表上我们只能根据X的边缘密度 $Pr(x=1)=\sum_{y}Pr(x=1,y)=0.024$ 来估计你的车被盗的风险，但是如果你要是告诉我，你的车型是3，那么你被盗  的可能性就是 $Pr(x=1,y=3)=0.001$ 了

所以，当一个联合分布中，我们知道一个随机变量x发生了，另一个随机变量y发生的概率从原来的$Pr(y)$ 变成了 $Pr(y|x)$ 而从相对关系上来看满足下面的关系：
$$
Pr(X=x|Y=y)=\frac{Pr(X=x \text{ and } Y=y)}{Pr(Y=y)}=\frac{f(x,y)}{f_2(y)}
$$

所以我们就能引出定义：
> Definition Conditional Distribution/p.f. Let X and Y have a discrete joint distribution eith joint p.f. $f$ .Let $f_2$ denote the marginal p.f. of Y Fot each y such that $f_2(y)>0$ ,define:
$$
g_1(x|y)=\frac{f(x,y)}{f_2(y)}
$$
>Then $g_1$ is called the conditional p.f. of X given Y.The discrete distribution whose p.f. is $g_1(\cdot |y)$ is called the conditional distribution of $X$ given that $Y=y$

定义大概就是上面的样子了，但是我们需要确认一下 $g_1(x|y)$ 这货到底是不是个分布，证明如下，假设 $f_2(y)>0$ ,$g_1(x|y)>0$ 那么对于所有 $x$ 来说:
$$
\sum_x g_1(x|y)=\frac{1}{f_2(y)}\sum_xf(x,y)=\frac{1}{f_2(y)}f_2(y)=1
$$

一个随机变量的概率分布必须满足所有值都大于0 ，$g_1(x|y)>0$ 满足条件，并且所有可能的概率和是1，上面式子也证明了，所以 $g_1$ 是一个概率分布，Q.E.D

举个计算的🌰 ：
![](./table3_4.png)
根据上面的数据计算p.f. of $Y$ given $X=2$
$$
g_2(y|2)=\frac{f(2,y)}{f_1(x=2)}=\frac{f(2,y)}{0.6}
$$
因为本🌰是个离散有限的，可以很容易的求出所有情况下的值：$g_2(1|2)=1/2$ $g_2(2|2)=0$  $g_2(3|2)=1/6$ $g_2(4|2)=1/3$

注意当边缘分布中对应的是0的情况，也就是分母是0的情况，是没有意义的，为什么？首先我们可以从代数的角度理解，分母不能为零，其次，我们从概率的角度理解，不可能发生的事件或随机变量概率是0，如果这个事件发生了，那么他就不可能有概率0，所以前后矛盾，分母不能为0。
## 连续条件分布 Continuous Conditional Distributions
上面说明白了离散情况下的条件分布，用到了前一篇中的边缘分布，那么连续情况下的条件分布会是什么样呢？
还是先举个🌰 ：
>一个工序需要两步完成，第一阶段需要Y分钟，整个过程需要X分钟（包括前面的Y分钟），假设X和Y满足下面的连续分布，joint p.d.f.如下：

$$
f(x,y)=
\begin{cases}
e^{-x}&\text{ for }0\leq y\leq x<\infty &\\
0 &\text{otherwise}&
\end{cases}
$$

当我们知道Y用了多久以后，我们就能重新评估X的分布，换句话说，当我们得知 $Y=y$发生时 求 $g_1(x|Y=y)$ 的分布

> Definition 3.6.2 p.d.f. :Let $X$ and $Y$ have a continuous joint distribution with joint p.d.f. $f$ and respective marginals $f_1$ and $f_2$ .Let $y$ be a value such that $f_2(y)>0$ .Then the conditional p.d.f. $g_1$ of $X$ given that $Y=y$ is defined as follows:
$$
g_1(x|y)=\frac{f(x,y)}{f_2(y)}\text{ for }-\infty<x<\infty
$$
For values of y such that $f_2(y)=0$ ,we are free to define $g_1(x|y)$ however we wish ,so long as $g_1(x|y)$ is a p.d.f. as a function of $x$

上面就是关于连续随机变量的条件pdf的定义，与离散情况下的条件p.f.的定义非常相似，但是需要注意的是，一个是p.d.f.一个是p.f. 这个就是本质的区别

>Theorem: For each $y$ , $g_1(x|y)$ defined in Definition 3.6.2 is a p.d.f. as a function of $x$

这个定理要证明的也是，经过我们一些列计算，得到的新的函数，是否满足p.d.f.的要求，证明如下：
1. $f_2(y)=0$ 分母是0，没有计算意义
2. $f_2(y)>0$ 明显有$g_1(x|y)\geq0$
3. if $f_2(y)>0$
$$
\int^{\infty}_{-\infty}g_1(x|y)dx=\frac{\int^{\infty}_{-\infty}f(x,y)dx}{f_2(y)}=\frac{f_2(y)}{f_2(y)}=1
$$
Q.E.D

定理为了确定我们一系列计算得到仍然是p.d.f，证明了三点性质（其实是2点），保证函数满足p.d.f.的基本需求。参考，[p.d.f.的定义](http://face2ai.com/Math-Probability-3-2-Continuous-Distribution/)

继续上面关于工序的例子,我们来计算条件分布，当已知 $Y=y$ 的时候我们知道 $x\geq y$所以计算边缘分布：
$$
f_2(y)=\int^\infty_{y}e^{-x}dx=e^{-y}
$$
对于所有的 $y>0$ :
$$
g_1(x|y)=\frac{f(x,y)}{f_2(y)}=\frac{e^{-x}}{e^{-y}}=e^{y-x},\text{ for }x\geq y
$$
当 $x<y$ 的时候 $g_1(x|y)=0$

这个例子暂时告一段落，我们下面展示一张图来可视化一下连续随机变量的条件分布，因为离散情况下很容易想象，所以我们把连续的随机变量表示一下：
![](./p_d_f.png)
看图说话，完整的曲面是二维随机变量的联合p.d.f. 那么其中一个切片 $x=x_0$ 或者  $y=y_0$ 都能得到一个切片，这个切片即使条件分布的一个伸缩，为什么是伸缩，因为其积分不是1，为了让他的积分为1，或者说正规化，我们需要给他一个系数：$\frac{1}{f_1(x)}$ 或者 $\frac{1}{f_2(y)}$ ，这样就能保证其积分为 $\int^\infty_{-\infty} \frac{f(x_0,y)}{f_1(x_0)}=1$ 或者 $\int^\infty_{-\infty} \frac{f(x,y_0)}{f_2(y_0)}=1$

一点需要注意，我们说过，p.d.f和pf的区别在于，p.d.f.的单点对应的函数值没有意义，其区间内的积分才能反映区间的概率，那么上述式子中 $f(x_0,y)$ 是0肯定没错了因为这个单变量函数没有体积，如果你还不明白，就看上面的图，并且确定二维随机变量只有一块区域内的体积才有意义，那么$x=x_0$ 确定的平面，不管怎么算体积都是0，也就是对应的概率是0.
那么实际上严谨的连续条件分布的定义应该是这样的：
$$
g_1(x|y)=lim_{\epsilon \to 0}\frac{\partial}{\partial x}Pr(X\leq x|y-\epsilon < Y \leq y+ \epsilon)
$$
是这样的一个极限，首先用到的是c.d.f.到p.d.f.的求偏导，然后是给了y一个小区间，使得积分有意义。

剩下的就是混合分布了，一个连续随机变量一个离散随机变量，做法也很简单，各算各的，互不干扰
> Definition Conditional p.f. or p.d.f. from Mixed Distribution: Let $X$ discrete and let $Y$ be continuous with joint p.f./p.d.f. f.Then the conditional p.f. of $X$ given $Y=y$ is defined by Eq.(3.6.2) and the conditional p.d.f of $Y$ given $X=x$ is defined by Eq.(3.6.3)

上面说的3.6.2 就是离散条件分布定义中的计算公式，同样的3.6.3就是连续条件分布定义中的计算公式。

## 总结
本文较前几篇有点短小，但是介绍的东西确实重要很多，Part II 介绍条件概率分布的构成，欢迎大家继续收看。





