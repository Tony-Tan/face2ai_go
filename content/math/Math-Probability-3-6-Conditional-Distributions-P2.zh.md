---
title: 【概率论】3-6:条件分布(Conditional Distributions Part II）
categories:
  - Mathematic
  - Probability
tags:
  - 乘法法则
  - 贝叶斯理论
  - 随机变量的全概率公式
toc: true
date: 2018-03-12 09:06:00
---

**Abstract:** 本文介绍联合分布的构建，也就是条件分布部分的扩展和应用
**Keywords:** 乘法法则，贝叶斯定理，随机变量的全概率公式

<!--more-->
# 条件分布
今天这篇是上一篇的后半部分，其实应该是一篇，但是上一篇由于长时间没写博客导致写作速度下降，所以不得已分成两篇，最近除了写概率的博客，还有数学分析的博客，CUDA系列的也在更新，所以有点要累吐血的感觉，同时还在学习数理统计，数理统计用的是陈希孺先生的概率论与数理统计的数理统计部分，看了二十几页，发现他说的90%我基本都能看懂，但是真的不知道为啥上大学的时候，有老师讲还一脸懵x，是我智商进化了？还是书本难度降低了？这个就不得而知了，除非把大学教材重新拿过来比较一下，那就有点浪费时间了，我的目标是学好数学去研究机器学习，而不是做教材点评，难道不是么？
## 条件概率乘法法则 Multiplication Rule for Conditional Probability
乘法法则我们在事件的概率部分学过了[传送到条件概率](https://face2ai.com/Math-Probability-2-1-Conditional-Probability/)，也是通过条件概率过度出来的，并且乘法法则相对于条件概率适用面更广，因为条件概率有除法计算，所以必然会对概率为0的分母有所忌惮，但是乘法法则无所谓，0可以随便来：
$$
Pr(A|B)=\frac{Pr(A,B)}{Pr(B)} \text{ for } Pr(B)\neq 0\\
Pr(A,B)=Pr(A|B)\times Pr(B) \text{ for } Pr(B)\geq 0
$$
根据随机变量的定义，我们知道随机变量是个函数，可以把事件映射成数字，如果我们将上面的条件概率转化成条件分布，应该怎么转呢？我们先看个例子
前面我们说过所有概率都是条件概率只是有些条件在题设中已经明确固定了，我们就没有必要再分布中再反复的体现了。
举个🌰：

1. 还是零件加工的问题，假设我们明确的知道加工这批零件的合格率是90%（我是怎么知道？上帝说的！就是知道，这也是概率论理想情况的抽象，就像物理中的质点一样），那么我们生产了100个零件，其中合格的零件为x个的事件的概率是多少：
分析，很简单的一个离散概率模型，设X是有零件x合格的事件，二项分布
$$
Pr(X=x)=\begin{pmatrix}100\\x\end{pmatrix}0.9^x(1-0.9)^{100-x} \text{ for }
$$

2. 那么这是我们的初级阶段，从初级到高级的一种变化方式就是把条件不确定化，比如上面的例子，我们条件中有两个已知数，90%和100 ，那么如果我们把100变成变量n呢？这个变量将会是一个普通的变量，或者说是输入变量，由我们自己决定。同时我们把事件转换到随机变量，那么例子就变成了
$$
g_1(x)=\begin{pmatrix}n\\x\end{pmatrix}0.9^x(1-0.9)^{n-x} \text{ for }x=0,1,2,\dots
$$
这种情况下，n是个普通可控制的变量，因为我们可以想象，如果你有一个工厂，生产一批零件，不管好坏，总数量肯定是你控制的，如果你控制不了，说明这个厂子你已经失去控制权了，也就是说，不管怎么样，这个n完全归我们管。那么我们下一步复杂。
3. 我们在1中蛮横不讲理的说90%是上帝告诉我们的，那么上帝是怎么知道这个数呢？《上帝掷骰子么》，那么如果他掷骰子这个事就又要归概率论处理了，那么我们接着引入变量p作为合格率(原始例子中的90%)，这个变量与n的最大差别是我们控制不了他，控制不了的就是随机的，随机的就可以用一个p.f.或者p.d.f来描述他，也就是说这个条件是要考虑其分布了，那么我们的例子近一步进化：
$$
g_1(x|p)=\begin{pmatrix}n\\x\end{pmatrix}p^x(1-p)^{n-x} \text{ for }x=0,1,2,\dots
$$
又因为我们上一篇已经研究过了离散，连续，混合随机变量的条件分布，那么这个例子很明显中p是连续的，x是离散的，是个混合条件概率，那么从概率转移到分布有：
$$
g_1(x|p)=\frac{f(x,p)}{f_2(p)}
$$
其中 $1\geq p\geq 0$
那么我们就有，X和P的联合p.f.或者p.d.f，若果我们假设$f_2(p)$ 是一个0到1区间内的均匀分布我们有：
$$
f(x,p)=g_1(x|p)f_2(p)=\begin{pmatrix}n\\x\end{pmatrix}p^x(1-p)^{n-x} \times f_2(p)\\
=\begin{pmatrix}n\\x\end{pmatrix}p^x(1-p)^{n-x} \times 1)=\begin{pmatrix}n\\x\end{pmatrix}p^x(1-p)^{n-x}\\
\text{ for }x=0,\dots ,n \text{ and } 0 \leq p \leq 1
$$
上面这个式子原文只给出：
$$
f(x,p)=g_1(x|p)f_2(p)=\begin{pmatrix}n\\x\end{pmatrix}p^x(1-p)^{n-x} \text{ for }x=0,\dots ,n \text{ and } 0 \leq p \leq 1
$$
看了半天才明白，他直接把1省略掉了，为啥是1 不知道？去看[分布的文章](https://face2ai.com/Math-Probability-3-2-Continuous-Distribution/)。

那么我们就可以正式的提出我们的定理了：

> Multiplication Rule for Distributions: Let $X$ and $Y$ be random variables such that $X$ has p.f. or p.f.d. $f_1(x)$ and $Y$ has p.f. or p.d.f $f_2(y)$. Also,assume that the conditional p.f. or p.d.f. of X given $Y=y$ is $g_1(x|y)$ while the conditional p.f. or p.d.f. of Y given $X=x$ is $g_2(y|x)$ .Then for each y such that $f_2(y)>0$ and each $x$,
$$
f(x,y)=g_1(x|y)f_2(y)
$$
where $f$ is the joint p.f. or p.d.f.,or p.f./p.d.f. of $X$ and $Y$ ,Similarly,for each $x$ such that $f_1(x)>0$ and each $y$,
$$
f(x,y)=g_2(y|x)f_1(x)
$$




上面公理虽然形式上和事件的条件概率很相似，但是注意他们的区别就是事件的概率公式中每个部分都是概率，而这里都是概率分布或者概率密度函数，一个是数，一个是函数，这个区别非常明显。
上面定理我们可以发现，两个边缘分布（也就是$f_1$ 和 $f_2$） 可以存在是0的情况，这并不影响什么，定理照样生效。
再举个🌰：
还是生产零件，假设我们生产了n个零件其中合格的比例是 $P=p$ 那么X个合格产品的分布是：
$$
f(x,p)=g_1(x|p)f_2(p)=\begin{pmatrix}n\\x\end{pmatrix}p^x(1-p)^{n-x} \text{ for }x=0,\dots ,n \text{ and } 0 \leq p \leq 1
$$

我们要计算在已知条件为 $X=x$ 时 $P$ 的分布 :
1. 计算边缘分布 $f_1(x)$ :
$$
f_1(x)=\int^1_0\begin{pmatrix}n\\x\end{pmatrix}p^x(1-p)^{n-x}dp
$$

2. 带入定理中的公式可以得到：
$$
g_2(p|x)=\frac{\begin{pmatrix}n\\x\end{pmatrix}p^x(1-p)^{n-x}}{\begin{pmatrix}n\\x\end{pmatrix}\int^1_0p^x(1-p)^{n-x}dp}\\
=\frac{p^x(1-p)^{n-x}}{\int^1_0p^x(1-p)^{n-x}dp}
$$

$\begin{pmatrix}n\\x\end{pmatrix}$ 是个常数，说以可以提出到积分外面，又因为其不为0，所以可以消去。
至此我们已经得到了通用解，但是我们为了好玩和形象，带入两个数进去看看，比如 $n=2,x=1$ 带入就有：
$$
\int^1_0p(1-p)dp=\frac{1}{2}-\frac{1}{3}=\frac{1}{6}
$$

那么

$$
g_2(p|1)=6p(1-p) \text{ for } 0\leq p \leq 1
$$
## 随机变量的贝叶斯定理，全概率计算 Bayes' Theorem and Law of Total Probability for Random Varibales
我们前面在事件条件概率之后提出之后也是提出了贝叶斯公式和全概率公式，那么我们还按照这个套路提出贝叶斯定理的分布形式，全概率公式的分布形式。
我们从事件到随机变量一路走过来，套路基本相同，逻辑相似，但是我们必须进行区分，毕竟随机变量是事件的函数过程，这样的过程是会造成很多不同的。我们后面也要时刻注意，不要再用事件的方法思考问题了，因为我们已经把事件数学化了。

>Theorem Law of Total Probability for Random Variables.If $f_2(y)$ is the marginal p.f. or p.d.f. of a random variabl $Y$ and $g_1(x|y)$ is the conditional p.f. or p.d.f. of $X$ given $Y=y$,then the marginal p.f. or p.d.f. of $X$ is
$$
f_1(x)=\sum_{y} g_1(x|y)f_2(y)
$$
if $y$ is discrete.If $y$ is continuous ,the marginal p.f. of p.d.f. of X given $Y=y$,then the conditional p.f. or p.d.f. of Y given $X=x$ is
$$
f_1(x)=\int^\infty_{-\infty}g_1(x|y)f_x(y)dy
$$

上面的定义同样适用于Y，这里就不再详细叙述了，理论推理就是乘法原理（乘法部分）加上边缘分布的算法（积分部分），就能得到随机变量的全概率分布。

> Bayes' Theorem for Random Variables.If $f_2(y)$ is the marginal p.f. or p.d.f. of a random variable $Y$ and $g_1(x|y)$ is the conditional p.f. or p.d.f. of $X$ given $Y=y$ ,then the conditional p.f. or p.d.f. of $Y$ given $X=x$ is
$$
g_2(y|x)=\frac{g_1(x,y)f_2(y)}{f_1(x)}
$$
where $f_1(x)$ can be obtained form 'Theorem Law of Total Probability for Random Variables' .Similarly,the conditional p.f. or p.d.f. of X given $Y=y$ is
$$
g_1(x|y)=\frac{g_2(x|y)f_1(x)}{f_2(y)}
$$
where $f_2(y)$ can be obtained form 'Theorem Law of Total Probability for Random Variables' .

上面连续给出两发定理，都是旧瓶装新酒，但是酒还是有区别的，从数字到函数，这个就是最大的变化。下面开始举例子。
举个🌰：
假设x是 $[0,1]$ 的均匀分布的随机变量，那么我们有：
$$
f_1(x)=
\begin{cases}1 & \text{for } 0<x<1\\
0 & \text{otherwise}
\end{cases}
$$
随机变量y是 $[x,1]$ 区间内的均匀分布，那么我们有，当 $X=x$ 给定的时候：
$$
g_2(y|x)=
\begin{cases}\frac{1}{1-x} & \text{for } x< y<1\\
0 & \text{otherwise}
\end{cases}
$$

那么根据乘法原理：
$$
f(x,y)=
\begin{cases}\frac{1}{1-x} \times f_1(x)=\frac{1}{1-x}  & \text{for } 0<x< y<1\\
0\times f_1(x)= 0 & \text{otherwise}
\end{cases}
$$

那么根据边缘分布的计算方法，可以得到y的边缘分布:
$$
f_2(y)=\int^\infty_{-\infty} f(x,y)dx=\int^y_0\frac{1}{1-x}dx=-log(1-y)
$$


## 独立随机变量 Independent Random Varibales
和事件独立套路依旧一致，随机变量的独立并不代表对立的你死我活，也不是说相交为空的互斥，而是相关的一种状态。
> Theorem Independent Random Variables.Suppose that $X$ and $Y$ are two random variables having a joint p.f.,p.d.f.or p.f./p.d.f. $f$ Then  $X$ and $Y$ are independent if and only if for every value of $y$ such that $f_2(y)>0$  and every value of $x$ ,
$$
g_1(x|y)=f_1(x)
$$

前面我们在[3.5](https://face2ai.com/Math-Probability-3-5-Marginal-Distributions/)中就提到过两个分布独立的充分必要条件就是$f(x,y)=f_1(x)f_2(y)$ 那么根据我们的乘法原理，我们知道$f(x,y)=f_2(y)g_1(x|y)$ 且 $f_2(y) \neq 0$ 那么$g_2(y|x)=f_2(y)$ 这样就证明了only if .
如果已知 $g_2(y|x)=f_2(y)$ 根据乘法原理，$f(x,y)=f_1(x)g_2(y|x)=f_1(x)f_2(y)$ if过程证明完成。

前面在事件的条件概率过程我们说过所有概率都是条件概率，没有条件就没有概率，只是有些条件我们不列出，或者不考虑，那么当我们要考虑某些条件的时候就出现了我们的条件概率，条件分布，但是我们具体操作者写条件概率和条件分布和普通的概率分布是一样的，因为他们都是条件的，只是有人写出来了，有人隐藏了。

## 总结
这一节分两篇看来分的还是挺正确的，不然一篇就太长了，我们下一篇继续。。。





