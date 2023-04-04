---
title: 【概率论】6-2:大数定理(The Law of Large Numbers)
categories:
    - Mathematic
    - Probability
tags:
    - 马尔科夫不等式
    - 切比雪夫不等式
    - 样本均值
    - 大数定理
toc: true
date: 2018-04-07 21:07:42
---

**Abstract:** 本文介绍马尔科夫不等式，切比雪夫不等式，样本均值，和大数定理的知识内容
**Keywords:** Markov Inequality，Chebyshev Inequality，Sample Mean，The Law of Large Numbers

<!--more-->
# 大数定理
最早做图像处理的时候建了一个QQ群，后来在里面认识了图像处理第一份工作的老板，后来离开了群，因为里面很多人基本都是来凑热闹的，所以质量堪忧，今天我又建了一个本博客的微信群，希望群内的同学们，能找到自己喜欢的方向，深入到自己热爱的领域，其实如果我的这些文字能帮助三五十个人，说实话，我自己感觉比那些小作坊身价过亿的小老板对社会的贡献更大一些。所以继续努力，戒骄戒躁。
想加入我们的同学，可以看目录页里面有进群的方法。


若干个拥有相同分布的独立随机变量的均值，被称为样本均值(“样本期望”等表述同一概念：**Sample Mean**)，这些被选取出来的随机变量被称为样本。样本均值对于样本的信息描述，类似于一个分布的期望对这个分布的描述。注意这句话有两个信息：
1. 我们前面介绍的均值，期望都是针对分布的。
2. 样本的均值不同于分布的均值，但是有很多相似之处。

本节我们就会介绍一些结果来表明，“样本均值”和“组成随机样本的单个随机变量”之间的关系。

## 马尔科夫不等式和切比雪夫不等式 The Markov and Chebyshev Inequalities
在学习均值的时候讲到过有关[重心](https://face2ai.com/Math-Probability-4-1-The-Expectation-of-a-Random-Variable-P1/)类似的概念，也就是说当我们改变分布，让小概率对应一个大的值的时候，比如离散情况下随机变量值 $\{1,100,0.1\}$ 对应于概率 $\{0.1,0.01,0.89\}$  这时的期望是 $1\times 0.1+100\times 0.01 + 0.1\times 0.89=1.189$ 也可以说重心在1.189这个位置，如果我们调整下，让大的随机变量值对应到大概率 $\{1,0.1,100\}$ 对应于概率 $\{0.1,0.01,0.89\}$ 这时的期望是 $1\times 0.1+0.1\times 0.01 + 100\times 0.89=89.101$ 显然这个重心发生了明显的偏移，但是我们有个新想法，如果我们有很多个离散随机变量值，或者是连续分布的随机变量，我们在固定分布均值的情况下，有多少随机变量值可以调整位置呢？
### 马尔科夫不等式 Markov Inequality
>Theorem Markov Inequality.Suppose that $X$ is a random variable such that $Pr(X\geq 0)=1$ .Then for every real number $t>0$ ,
$$
Pr(X\geq t)\leq \frac{E(X)}{t}
$$

证明思路的话我们就用一个离散分布来证明上面这个不等式的正确性然后延伸到连续情况。
证明：
1. 假设 $X$ 有一个离散分布，其p.f.是 $f$
2. 那么 $X$ 的期望是：
$$
E(X)=\sum_{x}xf(x)=\sum_{x<t}xf(x)+\sum_{x\geq t}xf(x)
$$
3. 因为我们在条件中规定 $X\geq 0$ 那么，上面的求和部分都是大于等于0的。
4. 所以我们有：
$$
E(X)=\sum_{x\geq t}xf(x)\geq \sum_{x\geq t}tf(x)=tPr(X\geq t)
$$
5. 根据 $t>0$ 得出我们要的结论：
$$
E(X)\geq t Pr(X\geq t)\Rightarrow  Pr(X\geq t)\leq\frac{E(X)}{t}
$$
6. 证毕

也就是说，Markov不等式回答了我们上面的问题，有多少随机变量值可以调整概率？对于某个正数 $t$ 调整前后必须满足大于 $t$ 的随机变量的全部概率要小于等于随机变量的期望除以 $t$ 这就是马尔科夫不等式给出我们的表面含义。
观察马尔科夫不等式，我们可以看出一个有趣的现象，如果 $t$ 是小于期望 $E(X)$ 的话，这个不等式就没啥意义了，因为概率必然小于1，所以多半情况下我们研究的是 $t > E(X)$ 的情况。
一个有趣的现象，如果一个随机变量的均值是1，那么其取到大于等于100的概率是 $Pr(X\geq 100)\leq \frac{1}{100}=0.01$
马尔科夫不等式得到概率和期望之间的关系，接下来我们想要看到的肯定是方差和概率之间的关系。
### 切比雪夫不等式 Chebyshev Inequality
方差是反应随机变量分布的离散情况（spread out）的描述。不等式表明，随机变量值与其均值之间的距离的概率受到其方差的制约，注意分析这句话的主语和定语。注意，今日主角大数定理的证明需要用到切比雪夫不等式。
>Theorem Chebyshev Inequality.Let $X$ be a random variable for which $Var(X)$ exists.Then for every number $t>0$ ,
$$
Pr(|X-E(X)|\geq t)\leq \frac{Var(X)}{t^2}
$$

看形势跟马尔科夫不等式很相似，所以证明也会用到马尔科夫不等式。
证明：
1. 设 $Y=[X-E(X)]^2$
2. 因为 $Y$ 是一个数的平方，那么我们有 $Pr(Y\geq 0)=1$
3. 根据方差的定义，有 $E[Y]=Var(X)$
4. 根据马尔科夫不等式，我们有 $Pr(Y\geq m)\leq \frac{E(Y)}{m}$ 其中 $m>0$
5. 因为想证明 $|X-E(X)|\geq t$ 形式下的关系，所以我们令 $t^2=m$
6. 所以 $Pr(Y\geq m)=Pr(|X-E(X)|\geq t)\leq \frac{E(Y)}{m}=\frac{Var(X^2)}{t^2}$
7. 所以得到最后结论 $Pr(|X-E(X)|\geq t)\leq \frac{Var(X)}{t^2}$
8. 证毕。

根据马尔科夫不等式给出的一些结论，在切比雪夫不等式中同样也是有响应的推论，比如我们令 $Var(X)=\sigma^2$ 以及 $t=3\sigma$ 那么我们的切比雪夫不等式就有：
$$
Pr(|X-E(X)|\geq 3\sigma)\leq \frac{\sigma^2}{(3 \sigma)^2}=\frac{1}{9}
$$

这个结论很有用，因为他刻画了一个分布要遵守的规则，就是超过 $3\sigma$ 的部分概率小于 $\frac{1}{9}$

## 样本均值的性质 Properties of the Sample Mean
样本均值的性质，首先我们还是来看样本均值的定义，样本均值还是一个随机变量，他是其他随机变量的线性组合，而组成他的这些变量必须是独立同分布的。
$$
\bar{X_n}=X_1+\dots+X_n
$$

注意，这里都是大写字母表示的是随机变量，而不是某个值，所以这个均值也是随机变量，接下来我们就要研究这个随机变量的性质了。
>Theorem Mean and Variance of the Sample Mean.Let $X_1,\dots,X_n$ be a random sample from a distribution with mean $\mu$ and variance  $\sigma^2$ .Let $\bar{X_n}$ be the sample mean.Then $E(\bar{X_n})=\mu$ and $Var(\bar{X_n})=\frac{\sigma^2}{n}$

证明虽然比较简单，我们还是证明一下比较好：
证明：
1. 根据[4.2](https://face2ai.com/Math-Probability-4-2-Properties-of-Expectations/) 中的定理
$$
E(\bar{X_n})=\frac{1}{n}\sum^{n}_{i=1}E(X_i)=\frac{1}{n}n\mu=\mu
$$
2. 根据[4.3](https://face2ai.com/Math-Probability-4-3-Variance/) 中方差的定理
$$
\begin{aligned}
Var(\bar{X_n})&=\frac{1}{n^2}Var(\sum^n_{i=1}X_i)\\
&=\frac{1}{n^2}\sum^{n}_{i=1}Var(X_i)\\
&=\frac{1}{n^2}\cdot n\sigma^2\\
&=\frac{\sigma^2}{n}
\end{aligned}
$$

换句话说，就是样本均值的期望会接近原始分布的期望，方差会变小，变小的比例是取样的数量，这个可以理解，因为你取的越少，离散程度自然越小。可以利用切比雪夫不等式来使得定理更加精确 因为$E(\bar{X_n})=\mu,Var(\bar{X_n})=\frac{\sigma^2}{n}$
$$
Pr(|\bar{X}-\mu|\geq t)\leq \frac{\sigma^2}{nt^2}
$$

-------------
举个🌰 ：
假设从一个分布中选取一个随机样本，均值 $\mu$ 未知，但是知道标准偏移 $\sigma$ 小于等于两个单位（2 units），那么我们需要至少多大的样本才能使得 $|\bar{X}-\mu|$ 小于1个单位的概率大于等于 0.99 。

注意，这里的2个单位，1个单位的表述方式是因为 方差没有单位，所以没办法说出量词
也就是说 $\sigma\leq 2\Rightarrow \sigma^2\leq 4$ 根据切比雪夫不等式：
$$
Pr(|\bar{X_n}-\mu|\geq 1)\leq \frac{\sigma^2}{n}\leq frac{4}{n}
$$
为了让 $Pr(|\bar{X}-\mu|<1)\geq 0.99$  必须使得 $\frac{\sigma^2}{n}\leq \frac{4}{n}\leq 0.01$ 这样就要求 $n$ 至少是 400 这个过程有问题的地方就是上面0.01和 $\frac{4}{n}$ 的关系这里，需要理清思路，切比雪夫不等式给出的不是最好的界限，因为其可能比最好的界限更严格，比如可能100个样本能解决，但是用切比雪夫算出来需要至少200个。

-------------
## 大数定理 The Law of Large Numbers
大数定理，大名鼎鼎，但是之前一直不知道他是干什么的，今天我们就来一起探索大数定理要表述什么，以及其背后的真相。
上面的例子用切比雪夫不等式来确定取样规模的大小，但是有些情况下确实有些虚报，比如其实只需要1000个样本，但是切比雪夫不等式得出的是10000个，这种情况经常发生，但是切比雪夫不等式绝对是个有用的工具，帮助我们证明下面的定理——“大数定理” ，大数不是指很大的数字，而是指很多的数字。
首先说说序列的收敛，这个在数学分析系列中会有严格的证明和解释，这里随机序列的收敛可以简单的理解为一个序列中的元素 $Z_n$ 在 $n$ 逐渐增加，$Z_n$ 逐渐接近某个实数 $b$ 的概率逐渐增大 ， 极限情况下 $lim_{n\to \infty}Z_n=b$ 发生的概率为1.

>Definition Convergence in Probability.A sequence $Z_1,Z_2,\dots$ of random variables converges to $b$ in probability if for every number $\varepsilon >0$ ,
$$
lim_{n\to\infty}Pr(|Z_n-b|<\varepsilon)=1
$$
This property is denoted by
$$
Z_n\xrightarrow{p} b
$$
and sometimes stated simply as $Z_n$ converges to $b$ in probability.

上面是极限的一种典型的定义方法，无论 $\varepsilon$ 多么小，都存在 $n$ 使得 $|Z_n-b|<\varepsilon$ 成立（概率的方法就是概率趋近于 1）。
换句话说，无论在 $b$ 附近多么小的区间，都存在当$n\to \infty$ 时 $Z_n$ 在此区间的概率趋近于1。

然后我们结合这个定义以及前面关于样本均值的定义，请出赫赫有名的“大数定理”

>Theorem Law of Large Numbers.Suppose that $X_1,\dots,X_n$ from a random sample from a distribution for which the mean is $\mu$ and for which the variance is finite.Let $\bar{X}_n$ denote the sample mean.Then
$$
\bar{X}_n\xrightarrow{p}\mu\tag{6.2.5}
$$

证明：
1. 对于每一个随机变量 $X_i$ ，我们设其方差为 $\sigma^2$
2. 根据切比雪夫不等式(变形)对于每一个 $\varepsilon>0$ 有：
$$
Pr(|\bar{X}_n-\mu|<\varepsilon)\geq 1-\frac{\sigma^2}{\varepsilon^2}
$$
3. 再根据样本的方差的性质 $Var(\bar{X}_n)=\frac{\sigma^2}{n}$
4. 那么因此有：
$$
Pr(|\bar{X}_n-\mu|<\varepsilon)\geq 1-\frac{\sigma^2}{n\varepsilon^2}
$$
5. 于是得到大数定理的结论：
$$
lim_{n\to \infty}Pr(|\bar{X}_n-\mu|<\varepsilon)=1\\
\bar{X}_n\xrightarrow{p}\mu
$$
6. 证毕

上述证明是在均值有限，方差有限的分布上进行证明的，当均值有限，方差无限的时候，需要用到更高深的方法进行证明。
大数定理有两种用法：
1. 当样本足够多的时候，样本均值和分布均值足够接近的概率非常大
2. 当样本足够多的时候，可以用样本均值来近似分布均值。

2中的用法将在下一篇继续讨论，进而引出中心极限定理，并且能够提出描述这两个均值之间的差。

>Theorem Continuous Functions of Random Variables.If $Z_n\xrightarrow{p}b$ ,and if $g(z)$ is a function that is continuous at $z=b$ ,then $g(Z_n)\xrightarrow{p}g(b)$

这个定理可以被扩展成多维情况：

>Corollary Continuous Functions of Random Variables.If $\vec{Z_n}\xrightarrow{p}\vec{b}$ ,and if $g(vec{z})$ is a function that is continuous at $\vec{z}=\vec{b}$ ,then $g(\vec{Z_n})\xrightarrow{p}g(\vec{b})$

这个定理的证明用到了随机变量的函数，和极限的函数两个知识点，这里不进行证明，具体可以参考[3.8](http://face2ai.com/Math-Probability-3-8-Fuctions-of-a-Random-Variable/)

>Theorem Histogram.Let $X_1,X_2,\dots$ be a sequence of i.i.d. random variables.Let $c_1 < c_2$ be two constants.Define $Y_i=1$ if $c_1\leq X_i<c_2$ and $Y_i=0$ if not .Then $\bar{Y}_n=\frac{1}{n}\sum^{n}_{i=1}Y_i$ is the proportion of $X_1,\dots,X_n$ that lie in the interval $[c_1,c_2)$ ,and $\bar{Y}_n \xrightarrow{p}Pr(c_1\leq X_1<c_2)$

在证明这个定理之前解释一下，这个定理是关于直方图的，对于一个随机样本（内包含多个i.i.d.的随机变量）其中落在某个固定区间上的个数与全部样本的个数的比例，概率趋近于原始分布在此区间的概率。这个定理存在的根本意义是证明了直方图可以反映原始分布形态！

证明：
1. 对于独立同分布的随机变量 $Y_1,Y_2,\dots$ 是独立同分布的伯努利随机变量
2. 根据伯努利分布的定义，其参数 $p=Pr(c_1\leq X_1< c_2)$
3. 根据大数定理，$\bar{Y}_n\xrightarrow{p}p$

这个定理直观的应用就是，一个随机样本中的随机变量值，落在范围 $[c_1,c_2)$ 内的比例概率趋近于这个分布在此区间的概率，这也就证明了，我们用落在某个范围内的随机变量的个数来刻画产生这些随机变量的分布在此区间的概率是受到大数定理的支持的。
上面这句话不好理解，可以多读几遍，或者定理的语言更直观！因为连续分布的p.d.f下的面积是对应区间的概率，所以我们经常用直方图的面积来表示这个区间的概率就是这么来的（有黎曼积分的思想在里面），作为进一步的近似，样本越多，直方图越接近原始分布。
以上全部定理，在条件分布下同样适用！
## 总结
本文介绍了大数定理，为了介绍大数定理，还介绍了马尔科夫不等式，切比雪夫不等式，样本均值方差，最后才引出大数定理，整个过程非常流畅，学完定理后需要多做练习。
明天继续中心极限定理。





