---
title: 【概率论】5-10:二维正态分布(The Bivariate Normal Distributions)
categories:
    - Mathematic
    - Probability
tags:
    - 二维正态分布
toc: true
date: 2018-04-05 22:03:55
---

**Abstract:** 本文介绍第一个多变量连续分布——双变量正态分布(<font color="ff0000">本篇内有未证明定理，需要后续要补充</font> )
**Keywords:** The Bivariate Normal Distributions

<!--more-->
# 二维正态分布
今天的废话想说说我们周围会有各种各样的事，各种各样的诱惑，各种各样的理由来告诉我们读书学习很苦而不学习也可以活的很好，但是坚持还是放弃只能选择一次，所以要慎重，开弓没有回头箭，放弃学习，就相当于放弃了一条抗争的路。
> 万般皆下品惟有读书高

今天我们来研究双变量的正态分布，多变量，连续分布。
对于某些研究者，可能用正态分布来非常好的描述某个随机变量，那么如果我们有两个随机变量，都可以用正态分布描述，而且他们之间存在关系，这时候我们就可以用一个双变量正态分布来描述了这两个变量之间的关系，并且这个二维分布的边缘分布，还是这两个随机变量单变量的分布。[5.6中](https://face2ai.com/Math-Probability-5-6-The-Normal-Distributions-P3/) 我们介绍了某些有正态分布的独立随机变量的线性组合还是正态分布。但是双变量正态分布（联合分布）可以是相关的。
## 二维正态分布的定义和来源 Definition and Derivation of Bivariate Normal Distributions
>Theorem Suppose that $Z_1$ and $Z_2$ are independent random variables,each of which has the standard normal distribution.Let $\mu_1,\mu_2,\sigma_1,\sigma_2$ ,and $\rho$ be constants such that $-\infty<\mu_i<\infty(i=1,2)$ , $\sigma_i>0(i=1,2)$  ,and $-1<\rho<1$ . Define two new random variables $X_1$ and $X_2$ as follows:
$$
X_1=\sigma_1Z_1+\mu_1\\
X_2=\sigma_2[\rho Z_1+(1-\rho^2)^{\frac{1}{2}}Z_2]+\mu_2 \tag{5.10.1}
$$
The joint p.d.f. of $X_1$ and $X_2$ is
$$
f(x_1,x_2)=\frac{1}{2\pi(1-\rho^2)^{\frac{1}{2}}\sigma_1\sigma_2}e^{-\frac{1}{2(1-\rho^2)}[(\frac{x_1-\mu_1}{\sigma_1})^2-2\rho(\frac{x_1-\mu_1}{\sigma_1})(\frac{x_2-\mu_2}{\sigma_2})+(\frac{x_2-\mu_2}{\sigma_2})^2]}
\tag{5.10.2}
$$

上面这个定理的证明需要定理3.9.5 ，而定理3.9.5是个选证题，也就是说会在我们后面的高级课程中进行证明，所以这个定理也就没法证明了，在证明了3.9.5 以后，我们会对此定理进行证明。
>Theorem Suppose that $X_1$ and $X_2$ have the joint distribution whose p.d.f. is given by Eq.(5.10.2) Then there exist independent standard normal random variables $Z_1$ and $Z_2$ such that Eqs (5.10.1) hold .Also,the mean of $X_i$ is $\mu_i$ and the variance  of $X_i$ is $\sigma_i^2$ for $i=1,2$ .Furthermore the correlation between $X_1$ and $X_2$ is $\rho$ .Finally,the marginal distribution of $X_i$ is the normal distribution with mean $\mu_i$ and variance $\sigma_i^2$ for $i=1,2$

此定理的证明也需要 3.9.5 的结论，所以我们目前只做不严谨的推理，两个联合分布如5.10.2，那么他们中的一个随机变量的分布（也就是联合变量的边缘分布）就是一个正态分布。均值和方差可求。

>Definition Bivariate Normal Distributions.When the joint p.d.f. of two random variables $X_1$ and $X_2$ is of the form in Eq(5.10.2),it is said that $X_1$ and $X_2$ have the bivariate normal distribution with mean $\mu_1$ and $\mu_2$ variance $\sigma_1^2$ and $\sigma_2^2$ ,and correlation $\rho$

以上就是第一部分要讲的内容，两个没证明的定理，和一个定义，这篇文章看起来有点水，确实是这样，但是如果没有知识又不完全，算是个占位符，但是双变量正态分布这个用途确实太多了，举个最简单的例子，我们的身高体重，就经常用双变量的正态分布来建模。
## 二维正态分布的性质 Properties of Bivariate Normal Distributions
接下来我们来研究一下双变量正态分布的性质
>Theorem Independence and Correlation.Two random variables $X_1$ and $X_2$ that have a bivariate normal distribution are independent if and only if they are uncorrelated.

两个随机变量有一个双变量正态分布，那么他们独立的充分必要条件是他们不相关。
来回忆一下[独立性](https://face2ai.com/Math-Probability-3-5-Marginal-Distributions/)和[相关性](https://face2ai.com/Math-Probability-4-6-Covariance-and-Correlation/)，独立性是两个随机变量分布之间满足 $f(x,y)=f_1(x)f_2(y)$ 这时 $X,Y$ 独立，不相关是说 $\rho(X,Y)=\frac{Cov(X,Y)}{\sigma_X^2\sigma_Y^2}=0$ 的时候两个变量不相关，[相关性(点击传送)](https://face2ai.com/Math-Probability-4-6-Covariance-and-Correlation/)的介绍中对于任何随机变量的分布，独立性都能推出不相关，但是不相关不能推出独立，所以为了证明本定理我们可以只证明，if过程，也就是不相关来推到独立，另一部分在相关性的文章中已经证明了。
证明 if 过程：
假设两个变量不相关，所以当 $\rho=0$ 从公式 5.10.2 中可以看出 $f(x_1,x_2)$ 可以被分解成两个分布相乘的形式，所以，我们可以得到这两个边缘分布独立。
证毕。
双变量的正态分布，不相关就独立，独立就不相关，在别的分布下不一定成立！
当相关性不为0的时候，我们会得到下面这个定理，就是一个变量再另一个变量给定情况下的分布。
>Theorem Conditional Distribution.Let $X_1$ and $X_2$ have the bivariate normal distribution whose p.d.f. is Eq.(5.10.2) .The conditional distribution of $X_2$ given that $X_1=x_1$ is the normal distribution with mean and variance given by
$$
\begin{aligned}
E(X_2|x_1)&=\mu_2+\rho\sigma_2(\frac{x_1-\mu_1}{\sigma_1})\\
Var(X_2|x_1)&=(1-\rho^2)\sigma_2^2
\end{aligned}
$$

当两个变量的联合分布为双变量正态分布，并且他们相关的时候，已知一个变量怎么来计算条件分布呢？
证明：
1. 给定条件 $X_1=x_1$ 等价于给定 $Z_1=\frac{x_1-\mu_1}{\sigma_1}$
2. 那么我们只需要证明给定条件 $Z_1=\frac{x_1-\mu_1}{\sigma_1}$ 下的 $X_2$ 的分布。
3. 那么把 $Z_1=\frac{x_1-\mu_1}{\sigma_1}$ 带入到式子 5.10.1中的第二个公式。
4. 那么给定条件 $X_1=x_1$ 下的 $X_2$ 的分布，等价于给定条件 $Z_1=\frac{(x_1-\mu_1)}{\sigma_1}$ 下，以下关系式的分布：
$$
(1-\rho^2)^{1/2}\sigma_2Z_2+\mu_2+\rho\sigma_2(\frac{x_1-\mu_1}{\sigma_1})\tag{5.10.7}
$$
5. 上式可见 $Z_2$ 是唯一的随机变量，并且 $Z_1$ 和 $Z_2$ 是独立的，所以 $X_2$ 在给定 $X_1=x_1$ 的条件下是 5.10.7 的边缘分布
6. 所以条件期望和条件方差如 5.10.6 所写。
7. 证毕

同理可以证明，
给定条件 $X_2=x_2$ 时 $X_1$ 的分布也是正态分布，并且其期望和方差如下
$$
E(X_1|x_2)=\mu_1+\rho\sigma_1(\frac{x_2-\mu_2}{\sigma_2})\\
Var(X_1|x_2)=(1-\rho^2)\sigma_1^2
$$

上面这两个结论可以看出，当两个变量相关的 $\rho\neq 0$ 时， $E(X_2|x_1)$ 是 $x_1$ 的线性函数，并且 $\rho$ 是斜率。并且此时条件方差是不依赖于条件的。条件方差比边缘概率的方差小，也就是说 $Var(X_1|X_2=x_2)< \sigma_2$ .

----------------
这里可以简单的给个🌰 的大概描述：
在一群人中进行建模，得到一个身高和体重的二维联合分布，是正态分布。已知一个人的身高预测他的体重，和不知道身高预测体重，是完全不同的两个过程，一个是条件期望，一个是边缘分布的期望，因为两个随机变量相关，所以必然用条件期望更准确一些（误差更小一点）。

---------------

## Linear Combination
线性组合我们只证明一个定理：
>Theorem Linear Combination of Bivariate Normals.Suppose that two random variables $X_1$ and $X_2$ have a bivariate normal distribution ,for which the p.d.f is specified by Eq.(5.10.2).Let $Y=a_1X_1+a_2X_2+b$ ,where $a_1,a_2$ and $b$ are arbitrary given constants .Then $Y$ has the normal distribution with mean $a_1\mu_1+a_2\mu_2+b$ and variance
$$
a_1^2\sigma_1^2+a_2^2\sigma_2^2+2a_1a_2\rho\sigma_1\sigma_2
$$

当两个变量的联合分布是双变量正态分布的时，其和是一个正态分布，并且期望和方差满足上述关系。

证明：
1. 依据双变量正态分布的定义，我们可以用 $Z_1$ 和 $Z_2$ 的线性组合来表示 $X_1$ 和 $X_2$ 的线性组合。
2. $Z_1$ 和 $Z_2$ 独立（已知条件）
3. $Y$ 可以表示成$Z_1$ 和 $Z_2$ 的线性组合
4. 根据5.6中推论 Y还是正态分布，并且期望为：
$$
\begin{aligned}
E(Y)&=a_1E(X_1)+a_2E(X_2)+b\\
&=a_1\mu_1+a_2\mu_2+b
\end{aligned}
$$
5. 根据4.6 中的推论： $Var(Y)=a_1^2 Var(X_1)+a_2^2 Var(X_2)+2a_1a_2 Cov(X_1,X_2)$
6. 证毕


## 总结
给出了两个变量的正态分布的定义（这个定理中给出了双变量正态分布的所有有用性质的根本），双变量正态分布的性质的证明主要用到这个定理（本篇第一个定理），所以本篇第一个定理是关键中的关键。





