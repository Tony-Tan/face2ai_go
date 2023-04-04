---
title: 【概率论】5-7:Gama分布(The Gamma Distributions Part II)
categories:
    - Mathematic
    - Probability
tags:
    - 指数分布
toc: true
markup: pandoc
date: 2018-04-02 09:16:46
---

**Abstract:** 本文介绍Gamma分布相关知识的第二部分指数分布
**Keywords:** The Exponential Distributions

<!--more-->
# Gama分布
怀疑是我们学习路上最大的绊脚石，因为学习完很多东西都不是立刻就能变现的，或者能直接在生活中能体现出变化的。所以能看长线的人，才适合进行长期学习，量变到质变的过程，而我们最重要的就是排除万难，坚定信念，至于结果如何，我相信古人的总结。
本文介绍的Gamma分布知识的第二部分有一个自己的名字，叫做指数分布，Gamma分布之所以叫Gamma分布是因为其中包含Gamma函数，而其中某个参数的特殊化产生的新分布，就是我们今天要学习的指数分布（The Exponential Distribution）。
指数分布一般用来建模等待时间等情况下的概率模型。
## 指数分布 The Exponential Distribution
我们上面一篇大讲特讲的服务时间例子，就是一个典型的等待时间的情况，所以，本文介绍的分布族可以用来进行建模
>Definition Exponential Distributions.Let $\beta >0$ .A random variable $X$ has the exponential distribution with parameter $\beta$ if $X$ has a continuous distribution with the p.d.f.
$$
f(x\beta)=
\begin{cases}
\beta e^{-\beta x}& \text{ for }x>0\\
0&\text{for} x\leq 0
\end{cases}
$$

这就是指数分布的定义，还是想之前说的，定义就是对这个在什么情况下分布是什么样子的进行定义，然后我们接下来要做的是通过这个定义能产生多少相关的定理结论。
作为对比，我们来列出Gamma分布，进行对比就能清楚地知道一些性质了，[Gamma分布](https://face2ai.com/Math-Probability-5-7-The-Gamma-Distributions-P1/)

<font face="黑体" color=#6F6FFF><B>
Gamma Distributions.Let $\alpha$ and $\beta$ be positive numbers.A random variable $X$ has the gamma distribution with parameters $\alpha$ and $\beta$ if $X$ has a continuous distribution for which the p.d.f. is
$$
f(x|\alpha,\beta)=
\begin{cases}
\frac{\beta^\alpha}{\Gamma(\alpha)}x^{\alpha-1}e^{-\beta x}&\text{ for } x>0\\
0&\text{otherwise}
\end{cases}
$$
</B></font>

因为Gamma函数在 $\Gamma(1)=1$ 所以，指数分布就是Gamma分布 $\alpha=1$ 的时候产生的分布。

>Theorem The exponential distribution with parameter $\beta$ is the same as the gamma distribution with parameters $\alpha=1$ and $\beta$ .If $X$ has the exponential distribution with parameter $\beta$ ,then
$$
E(X)=\frac{1}{\beta}\text{ and } Var(X)=\frac{1}{\beta^2}
$$
and m.g.f. of $X$ is
$$
\Psi(t)=\frac{\beta}{\beta-t}\text{ for } t<\beta
$$


这个证明就不需要了，因为完全就是Gamma分布的代数结果，所以我们还是看点有用的性质吧，比如说，无记忆性。

>Theorem Memoryless Property of Exponential Distributions.Let $X$ have the exponential distribution with parameters $\beta$ ,and let $t>0$ .Then for every number $h>0$ ,
$$
Pr(X\geq t+h|X\geq t)=Pr(X\geq h)
$$

证明:
对于每一个 $t>0$ ,
$$
Pr(X\geq t)=\int^{\infty}_{t}\beta e^{-\beta x}dx=e^{-\beta t}\tag{5.7.19}
$$
那么对于每一个 $t > 0$ 以及 $h > 0$ 我们有
$$
\begin{aligned}
Pr(X\geq t+h|X\geq t)&=\frac{Pr(X\geq t+h)}{Pr(X\geq t)}\\
&=\frac{e^{-\beta(t+h)}}{e^{-\beta t}}=e^{-\beta h}=Pr(X\geq h)
\end{aligned}\tag{5.7.20}
$$

证明过程只用到了条件分布的求法，其他基本没有任何难度，这个结论是显然成立的。

值得说明的是，指数分布是在连续随机变量里面唯一一个就有无记忆性的分布；为了说明无记忆性，我们来看看思路：假设 $X$ 表示某个任务触发前的等待时间，根据式5.7.20 如果从时间0开始计时前t个时间单位没有任务触发，那么在接下来 $h$ 个时间单位触发任务的概率为 $e^{-\beta h}$  这个概率和从时间 $0$ 开始计时前 $h$ 个时间周期触发任务的概率一致.

但是必须要说明的是，无记忆性并不只是适合所有场景，比如假设 $X$ 是 **一个** 灯泡的的寿命，就是他坏掉之前持续点亮的时间，这个灯泡以后能点亮的时间完全取决于已经点亮了多久,因此单一灯泡不具有无记忆性，但是指数分布可以很好的近似产品或者零件的寿命。
下面我们就看看如何使用指数分布来建模使用寿命。

## 使用寿命测试 Life Tests
🌰 ：
假设有 $n$ 个灯泡点亮，来模拟检测他们的使用寿命，我们假设他们每个的使用寿命相互独立，并且有相同的分布，参数为 $\beta$ 的指数分布，换句话说，如果 $X_i$ 定义第 $i$ 个灯泡的寿命 $i=1,2,\dots,n$ 然后假设他们是i.i.d的，那么第一个问题，就是我们假设 $Y_1$ 是 $n$ 个灯泡中第一个坏掉的灯泡点亮的时间，那么其分布是什么样的？那么第二个坏掉的灯泡点亮的时间 $Y_2$ 又是怎么分布的呢？
分析：例子中 $Y_1$ 的分布式 $n$ 个指数分布随机变量中最小的，那么其分布应该比较容易计算。

>Theorem Suppose that the variables $X_1,\dots,X_n$ form a random sample from the exponential distribution with parameter $\beta$ .Then the distribution of $Y_1=min{X_1,\dots,X_n}$ will be the exponential distribution with parameter $n\beta$

定理说，n个独立同分布的指数分布的随机变量中最小的那个的新随机变量的分布是参数是 $n\beta$ 的指数分布。

证明：
对于每一个 $t>0$ 那么：
$$
\begin{aligned}
Pr(Y_1>t)&=Pr(X_1>t,\dots,X_n>t)\\
&=Pr(X_1>t)\dots Pr(X_n>t)\\
&=e^{-\beta t}\dots e^{-\beta t}=e^{-n\beta t}
\end{aligned}
$$
根据计算过程5.7.19可以比较轻松地得到上述结论。

根据无记忆性，对于例子中 $Y_2$ 的求法相当于从n个灯泡中有一个已经坏了的情况下，从新开始进行指数分布，也就是说当第一个灯泡坏了以后，我们重新开始进行试验，此时的时间归为0，那么参数变成了 $n-1$ 个灯泡，我们假设其中 第 $j$ 个灯泡先坏掉( $1<j<n$ ) 那么第二个坏掉的分布就是参数为 $(n-1)\beta$ 的指数分布。

那么我们接下来就有研究每次灯泡熄灭之间的时间间隔了。
>Theorem Suppose that the variables $X_1,\dots,X_n$ form a random sample from the exponential distribution with parameters $\beta$ .Let $Z_1\leq Z_2\dots \leq Z_n$ be the random variables $X_1,\dots,X_n$ sorted from smallest to largest.For each $k=2,\dots,n$ ,let $Y_k=Z_k-Z_{k-1}$ ,Then the distribution of $Y_k$ is the exponential distribution with parameter $(n+1-k)\beta$

上述定理说明指数分布的随机变量 $X_1,\dots,X_n$ 有参数 $\beta$ 那么假设 $Z_1\leq Z_2\dots \leq Z_n$ 是 $X_1,\dots,X_n$ 从小到大的排列 ，对于每一个 $Y_k=Z_k-Z_{k-1}$ 其中$k=2,\dots,n$ 那么  $Y_k$也是指数分布，并且其参数是  $(n+1-k)\beta$ 。

这个看起来就有点神奇了，但是证明过后发现，确实如此。
证明：
在时间 $Z_{k-1}$ ，有 $k-1$ 个寿命已经结束了，有 $n+1-k$ 个还没坏，那么根据上一个例子，剩下的活着的的依然遵守无记忆性性质，依然服从指数分布，其参数为 $\beta$ ，所以 $Y_k=Z_k- Z_{k-1}$ 也是活着的最小寿命时间分布，还是参数为 $\beta$ 的指数分布，只不过试验总数变成了 $n+1-k$ 个，所以根据定理 5.7.10 指数分布参数为 $(n+1-k)\beta$
接下来我们研究一下，泊松过程和指数分布之间的关系。
## 指数分布和泊松过程的关系 Relation to Poisson Process
回顾下[泊松分布](https://www.face2ai.com/Math-Probability-5-4-The-Poisson-Distribution/)的提出，当时提出泊松分布的情况是为了计算某段时间内到达商店的顾客数量，当时假定平均每个小时有多少人，然后按照伯努利过程抽象最小时间单位比如秒内是否有人来，然后得出一段时的二项分布，发现二项分布太麻烦，于是用泊松分布来近似此情况下的二项分布，用于建模某段时间内的客户数量，但是，当我们想要知道每两个相邻进店的客户之间间隔了多少时间，这时候就可以用指数分布来进行建模了

>Theorem 5.7.12 Times between Arrivales in a Poisson Process.Suppose that arrivals occur according a Poisson process with rate $\beta$ .Let $Z_k$ be the time until the $k$ th arrival for $k=1,2,\dots$ .Define $Y_1=Z_1$ and $Y_k=Z_k-Z_{k-1}$ for $k\geq 2$ Then $Y_1,Y_2,\dots$ are i.i.d. and they each have the exponential distribution with parameter $\beta$

证明，假设泊松分布的变量为 X ，那么当 $Y_1\leq t$ 时对应的 $X\geq 1$ 应该等于 $1-Pr(X=0)=1-e^{-\beta t}$ 可以看出上式是指数分布的c.d.f。其参数是 $\beta$

泊松过程中，两个到达之间的时间可以用指数分布来建模。

根据定理5.7.7 和 5.7.12 可以得出以下推论。
>Corollary Time until $k$ th Arrival. In the situation of Theorem 5.7.12,the distribution of $Z_k$ is the gamma distribution with paramters $k$ and $\beta$

## 总结
本文在上文Gamma分布上进行特例，得到一中经常由于建模使用寿命，或者泊松过程时间间隔的分布——指数分布。
下一篇我们继续啊在Gamma分布的基础上构建其他类型的分布。
待续。。。





