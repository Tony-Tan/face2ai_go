---
title: 【概率论】4-1:随机变量的期望(The Expectation of a Random Variable Part II)
categories:
    - Mathematic
    - Probability
tags:
  - 期望
toc: true
date: 2018-03-22 09:09:37
---

**Abstract:** 本篇介绍期望的第二部分，关于随机变量的函数的期望
**Keywords:** Expectation

<!--more-->
# 随机变量的期望
本来这篇可以和前一篇合在一起的，但是看了下还是有点长，控制下篇幅来保证质量，有的时候追求多快就会影响到质量。
## 函数的期望 The Expecatation of a function
一个函数的期望，首先这个函数一定是个随机变量的函数，那么其结果也是个随机变量，是随机变量就有分布，所以就有可能有期望。
举个🌰 ：
一个家电制造公司制造的电器每年出现故障的比率是 $X$ ，$X$ 是一个当前不知道的随机变量，如果我们感兴趣的是这个电器是失效前能运行多久，我们可能会使用 $1/X$ 来表示这个时间，那么我们计算 $Y=1/X$ 的平均值呢？
这就是我们今天要讨论的问题，如何求一个关于随机变量函数的期望。
### 单随机变量的函数 Function of a Single Random Variable
首先来看函数的自变量只有一个随机变量的情况。
> Function of a Single Random Variable : If $X$ is a random variable for which the p.d.f. is $f$ ,then the expectation of each real-valued function $r(X)$ can be found by applying the definition of expectation to the distribution of $r(X)$ as follows:Let $Y=r(X)$ ,determine the probability distribution of $Y$ ,and then determine $E(Y)$ by applying either expectation for a discrete distribution or expectation for a continous distribution.For example suppose that $Y$ has a continuous distribution with the p.d.f. $g$ .Then
$$
E[r(X)]=E(Y)=\int^{\infty}_{-\infty}yg(y)dy
$$

这段文字的意思就是，一个随机变量的函数会产生一个新的随机变量，新的随机变量会有分布，这个分布如果有期望，那么就可以按照期望的原始定义计算这个新的随机变量的期望，也就是老随机变量的函数的期望了。
所继续上面的例子，如果 $X$ 的p.d.f.是：
$$
f(x)=
\begin{cases}
3x^2&\text{ if }0<x<1\\
0&\text{oterwise}
\end{cases}
$$

那么根据上面例子的关系 $r(x)=\frac{1}{x}$，我们可以得到 $Y=r(x)$ 的p.d.f.：
$$
g(y)=
\begin{cases}
3y^{-4}&\text{ if }y>1\\
0&\text{oterwise}
\end{cases}
$$
那么Y的期望就是：
$$
E(Y)=\int^{\infty}_{0}y^3y^{-4}dy=\frac{3}{2}
$$

>Theorem Law of the Unconscious Statistician.Let $X$ be a random varibale,and let $r$ be a real-valued function of a real variable.If $X$ has a continuous distribution,then
$$
E[r(x)]=\int^{\infty}_{-\infty}r(x)f(x)dx
$$
If the mean exists.If X has a discrete distribution ,then
$$
E[r(X)]=\sum_{\text{All } x}r(x)f(x)
$$
if the mean exists.

这个定理的名字翻译成中文非常尴尬，叫“未知统计家法则” ，哪部分是未知的？明显自变量随机变量的分布已知，和新的随机变量的关系 $r$ 也是已知，而新的随机变量的分布是未知，所以我觉得未知应该就是指的是新随机变量的分布，这个分布是不需要求出来就能求期望的，这一点是很神奇的，而计算方法从公式上的体现就是直接用$r(x)$ 替换掉了以前的 $x$ 而p.d.f还是用原始的$x$ 的p.d.f.
我们可以证明下上面的这个定理，我们只证明离散情况的，连续情况下的大家可以自己证明。
证明：
假设X的分布式离散的，那么Y的分布必然也是离散的，我们来使 $g$ 为 $Y$ 的 p.d.f. 那么
$$
\sum_{y}yg(y)=\sum_{y}yPr[r(x)=y]\\
=\sum_{y}y\sum_{x:r(x)=y}f(x)\\
=\sum_{y}\sum_{x:r(x)=y}r(x)f(x)=\sum_{x}r(x)f(x)
$$
Q.E.D

证明过程中最关键的一步是 $Pr[r(x)=y]=\sum_{x:r(x)=y}f(x)$ 这一步是把原始随机变量和新随机变量联系起来的关键步骤，然后根据加法分配原理，把 $y$ 塞到求和公式里面，用 $r(x)$ 做代换，就得到了$\sum_{x:r(x)=y}r(x)f(x)$ 最后是合并两个求和，第一个求和是按照变量y来求，而里面的是根据满足y的所有x的求和，那么综合起来就是求所有x的集合，因为每个x都要被映射成一个y，举个例子，因为这个式子还是有点难度的，你有三个盒子，每个盒子里有不同的若干块糖，你要做的是先把每个盒子里糖数出来，然后再把每个盒子的糖的数量加起来求总数量，和你把所有糖都集中起来，计数，结果是一样的。

知识点完毕按道理来说，这里应该多看几个例子。

注意： $E[g(x)]\neq g(E[x])$
### 多随机变量的函数 Function of Several Random Variables
同样的问题，如果上面的r对应的自变量随机变量不是一个随机变量呢？已知随机变量 $x$ 和 $y$ 的分布，那么求随机变量 $Z=X^2+Y^2$ 的期望，这事怎么办？
继续我们的尴尬😓 定理
>Theorem Law of Unconscious Statistician:Suppose $X_1,\dots,X_n$ are random variables with the joint p.d.f $f(x_1,\dots,x_n)$ Let $r$ be a real-valued function of $n$ real varibales,and suppose that $Y=r(X_1,\dots,X_n)$ .Then $E(Y)$ can be determined directly from the relation
$$
E(Y)=\underbrace{\int\dots\int}_{R_n}r(x_1,\dots,x_n)f(x_1,\dots,x_n)
$$
if the mean exists.Similarly ,if $X_1,\dots,X_n$ have a discrete joint distribution with p.f. $f(x_1,\dots,x_n)$ the mean of $Y=r(X_1,\dots,X_n)$ is
$$
E(Y)=\sum_{\text{All }x_1,\dots,x_n}r(x_1,\dots,x_n)r(x_1,\dots,x_n)f(x_1,\dots,x_n)
$$
if the mean exists

没错，就是上面单变量的扩展版本。证明过程也是一样的，就是把单变量改成向量而已，基本没有难度，甚至如果你对线性代数很了解，基本上就是把一定范围的数的求和引申的某个空间上所有向量的求和，然后就能得出结论，连续情况下，积分同理！


## 总结

期望是一个分布的一个非常重要的属性，分布确定就能确定唯一的期望，这种一对一的关系也好，或者是其本身含义也好，都决定了其在概率学中的重要地位，我们本章学的基本都是分布的一些数字性质，而且都是用期望作为基础得到的，我们后面继续。。。





