---
title: 【线性代数】6-6:相似矩阵(Similar Matrices)
categories:
  - Mathematic
  - Linear Algebra
tags:
  - 相似矩阵
  - 特征值
  - 特征向量
toc: true
date: 2017-11-29 09:08:12
---

**Abstract:** 本文主要介绍根据矩阵对角化以及特征值引出的相似矩阵的性质和特点
**Keywords:** Similar Matrices,Jordan Form,Eigenvalues,Eigenvectors

<!--more-->
# 相似矩阵
特征值特征向量这一章是线性代数的高潮部分，可以说是高潮迭起，这部分相比四个子空间部分可能逻辑性更强一点，需要前后联通，只看一部分肯定要掉坑，所以这几篇写的都非常多，今天的相似矩阵是对角化引出的另一个重要分支，但是篇幅不大。
在研究这一章的时候总感觉Prof. Strang写的很细致，可以很容易的帮你知道什么是什么但是如果想了解点深入的背后的东西，由于篇幅限制（可以看出老先生有意的控制篇幅，并没有长的长的短的短，所有章节长度基本相同）没有深入讨论，也可能线性代数的introduction仅限于这些，更深入的话可能就是另一门课了，所以后续可能出个矩阵论或者矩阵分析类的系列博客。

## 相似矩阵(Similar Matrices)
Similar相似，但又不同，如果说某两件事物相似，那么必然有相似点，也就是这两件事物的某一属性，或者某几个属性一致，那么如果说两个矩阵相似，有可能是形状，比如上三角矩阵，对角矩阵，这些矩阵都有相同的属性，我们这里定义矩阵相似--拥有相同的特征值。

本章我们研究的主要内容是矩阵的对角化，对角化的前提是有足够的特征向量，也就是说如果某个矩阵特征向量不足，那么就没办法产生特征向量矩阵$S$ 那么我们就不研究他们了，😁我们这里不研究特征向量不够的情况，同样，本文中我们也是研究有足够特征向量的矩阵，如果矩阵$A$ invertible,那么可逆矩阵$M$ 构成的$MAM^{-1}$ 的新矩阵是 $A$ 的相似矩阵，因为$M$ 的多样性，所以相似矩阵不是唯一的相反的，应该是一群（family）。

> Definition: Let $M$ be any invertible matrix.Then $B=M^{-1}AM$ is similar to $A$

因为我上面剧透了，相似矩阵是有相同特征值的矩阵，但是如果我们不知道这个性质，我们来观察下面这个过程,假设矩阵 $M$ 可逆：
$$
B=M^{-1}AM\\
A=MBM^{-1}\\
set:\;N=M^{-1}\\
then:\;N^{-1}=M\\
A=N^{-1}BN
$$

要说的是 $B=M^{-1}AM$ 和 $A=N^{-1}BN$ 无论是长相和性质都极为相似，那么根据定义A相似与B，B也相似与A，所以相似是个可逆的，即可以反过来的。
对角化后的 $\Lambda$ h和原始矩阵A也是相似的，当$M=S$ 的时候，使得相似矩阵B变成了 $\Lambda$

线性代数和微分方程关系紧密（线性代数是基础学科，所以跟基本谁都有关系），比如对于微分方程 $\frac{du}{dt}=Au$ ,我们对变量 $u$ 进行代换 $u=Mv$ 其中M是可逆的常数矩阵：
$$
\frac{du}{dt}=Au\\
\frac{dMv}{dt}=AMv\\
M\frac{dv}{dt}=AMv\\
\frac{dv}{dt}=M^{-1}AMv
$$

通过代换u和v，我们得到了A的一个相似矩阵，也可以通过将M变成S，这样得到的系数矩阵就是对角矩阵，其实前面有一篇专门讲微分方程的课我们略过了，实际上特征值是可以反应出系统是逐渐偏向增加还是减少的（这个地方听不懂没关系，因为出来的太突然了，没有一点点防备，你就这样出现。。）所以相似矩阵必然有一样的特征值，这样才能进行代换后，不影响系统原始的变化方式，那么，又是那句话，相似矩阵家族的特征值是相同的不然不相似。

下面的关键就是证明特征值没变,假设矩阵A是可对角化的矩阵。

$$
A=S_A\Lambda S_A^{-1}\\
B=M^{-1}AM\\
B=M^{-1}S_A\Lambda S_A^{-1}M\\
B=(M^{-1}S_A)\Lambda (M^{-1}S_A)^{-1}\\
S_B=M^{-1}S_A\\
B=S_B\Lambda S_B^{-1}
$$

可见B和A的特征值是不变的，然后特征向量矩阵要乘以系数矩阵 $M^{-1}$ ，所以下面这个过程是等价的：
$$
B=M^{-1}AM\\
Bx=\lambda x\\
M^{-1}AMx=\lambda x\\
AMx=M\lambda x\\
AMx=\lambda (Mx)\\
set:\; y=Mx\\
Ay=\lambda y
$$

又一次证明了相似矩阵的特征值不变，同时特征向量变化等于 $Mx$ 就是原始特征值乘以了系数矩阵。这里面还有一个隐藏的坑，就是特征值相等的时候，如果矩阵A有n个相等的特征值 $\lambda$，那么B重也有n个相等的特征值 $\lambda$ 。这种情况有些困难，下面开始举🌰 ：
$$
A=\begin{bmatrix}0.5&0.5\\0.5&0.5\end{bmatrix}\\
S_A=\begin{bmatrix}1&1\newline -1&1\end{bmatrix}\\
S_AAS_A^{-1}=\begin{bmatrix}1&0\\0&0\end{bmatrix}\\
Chose:\\
M=\begin{bmatrix}1&0\\1&-2\end{bmatrix}\\
then:\\
B=M^{-1}AM=\begin{bmatrix}1&-1\\0&0\end{bmatrix}\\
S_B=\begin{bmatrix}1&1\\0&1\end{bmatrix}\\
S_B^{-1}=\begin{bmatrix}1&-1\\0&1\end{bmatrix}\\
S_BBS_B^{-1}=\begin{bmatrix}1&0\\0&0\end{bmatrix}
$$

可以通过简单的计算得到与证明中一致的结论，本例子和书中有写区别，用octave进行了验证，可以放心使用

下面再举一个比较困难的🌰就是两个特征值相等的情况。
$$
A=\begin{bmatrix}0&1\\0&0\end{bmatrix}\\
\lambda_1=0\\
\lambda_2=0\\
$$
这样的话两个特征值都为0，那么特征向量就是A的0空间，又因为矩阵的rank是1，也就是说nullspace的dimension是1，所以两个特征值对应一个个方向上的特征向量,$S=\begin{bmatrix}1&1\\0&0\end{bmatrix}$ 不可逆， A不能对角化，但是我们依然可以找到可逆矩阵$M=\begin{bmatrix}a&b\\c&d\end{bmatrix}$ 他的逆是$M^{-1}=\frac{1}{ad-bc}\begin{bmatrix}d&-b\newline -c&a\end{bmatrix}$ ，那么我们就能得出一个通用的框架，满足$B=M^{-1}AM$ 的所有矩阵与A相似，虽然A没有足够的特征向量（文章开始说不研究的，但是还是被带进坑了）

$$
B=\frac{1}{ad-bc}\begin{bmatrix}d&-b\newline -c&a\end{bmatrix}\begin{bmatrix}0&1\\0&0\end{bmatrix}\begin{bmatrix}a&b\\c&d\end{bmatrix}=\begin{bmatrix}cd&d^2\newline -c^2&-cd\end{bmatrix}
$$
满足上述公式的所有B（必须可逆，也就是行列式要不等于0）都是A的相似矩阵，当然这个特殊的例子也要强调一下：**除了** $\begin{bmatrix}0&0\\0&0\end{bmatrix}$ ，这个家伙比较讨厌也不可逆，所以我们把它排除了。观察上面B，发现trace是0，行列式也是0，满足检验。
B是A的一个通用版本，但是可以看出没办搞成对角矩阵，A已经是最接近对角矩阵的了，我们把A称作是这个family的Godfather，或者学术一点叫做 Jordan Form，后面我们会大概的介绍Jordan form更多内容要看进阶篇了。

这是一个比较特殊的例子，特征向量不够的情况，但是不论够不够，相似矩阵总有下面这些性质

|          Not changed by M          |  Changed by M  |
|:----------------------------------:|:--------------:|
|            Eigenvalues             |  Eigenvectors  |
|       Trace and determinant        |   Nullspace    |
|                Rank                |  Column space  |
| Number of independent eigenvectors |   Row space    |
|            Jordan form             | Left nullspace |
|                                    | Sigular values |

一条一条分析，首先特征值不变，我们已经论证过了，同时也知道特征向量发生了变化，特征值不变以为着Trace和determinant的不变（因为他们和特征值之间有数值关系，所以特征值不变这两个可能不变）；***Nullspace发生了变化，因为Nullspace是特征值为0的时候的特征向量span的space，如果特征向量发生变化，那么Nullspace肯定也发生了变化，这里有点疑问，如果M是identity呢？*** ；Rank是不变的，因为如果特征值不变，0特征值的个数就不变，这样nullspace的维度就不变，那么rank不变；与nullspace同理，非零特征值对应的特征向量发生改变，其span的column space就会发生改变；independent的特征向量的数量不会发生变化，因为对应的子空间的维度不变，所以线性独立的特征向量（也就是子空间的一组基的数量）不会发生变化；row space发生变化，因为行空间的基都乘以了M；Jordan不变，因为不改变相似性，在整个家族中Jordan是最接近对角矩阵的，所以不会发生改变；left nullspace随着行空间改变而被改变；Singular values会改变，这个下一篇会讲到，这里大家还不太明确奇异值是什么。

## 乔丹形式的例子(Examples of the Jordan form)
Jordan Form上文说是最接近对角矩阵的矩阵，这句话有个问题，就是如何评价什么“接近”，也就是没有一个统一的标准，来计算一个矩阵和对角矩阵的差别有多大。所以我们在这段和下一段找找根据，这段主要是🌰 ：
Jordan Matrix J:
$$
J=\begin{bmatrix}5&1&0\\0&5&1\\0&0&5\end{bmatrix}\\
then:\\
J-5I=\begin{bmatrix}0&1&0\\0&0&1\\0&0&0\end{bmatrix}
$$
所有与J相似的矩阵B都有三个一样的特征值5，并且 $B-5I$ 的rank不变（是2），也就是nullspace是1，这样的矩阵B与J相似（**这里有个问题，就是在确定特征值相等后，还有反复确认rank和nullspace，这个也是这里第一次见，后面可能有更具体的解释**）

>Jordan Theorem :$J^T$ 和 $J$ 相似

$$
J^T=M^{-1}JM=
\begin{bmatrix}&&1\\&1&\\1&&\end{bmatrix}
\begin{bmatrix}5&0&0\\1&5&0\\0&1&5\end{bmatrix}
\begin{bmatrix}&&1\\&1&\\1&&\end{bmatrix}
$$
数值上支持了理论，但是Jordan Theorem具体内容还应该具体的证明，例子只是从表面上让大家知道说的是什么，但本身没有证明真伪的意义。

另一个例子，这个例子是微分方程，与上面提到的一样，这里不再具体描述了，但是要记住：
对变量 $u$ 进行代换 $u=Mv$ 其中M是可逆的常数矩阵：
$$
\frac{du}{dt}=Au\\
\frac{dMv}{dt}=AMv\\
M\frac{dv}{dt}=AMv\\
\frac{dv}{dt}=M^{-1}AMv
$$

这里是对输入，或者是初始状态进行了变换，下一章将对基进行变化（也就是一个动坐标值，一个动坐标轴）。

## 乔丹形式(The Jordan Form)
接下来详细的介绍下Jorda Form也就是Jordan形式，没有详细的推到过程，因为对Jordan形式的严格证明书中就没有，也不是线性代数初级部分的内容，我们要知道的就是Jordan的具体形式，以及部分用途，Jordan存在的最大意义就是解决不能对角化的矩阵在需要对角化的时候的引发的问题，也就是Jordan Form 是更广义的对角化，而之前我们讲的拥有足够特征向量的方阵的对角化只是Jordan Form的一种特例而已，Jordan是更广泛的方式。

【宏观】Jordan Form：
$$
M^{-1}AM=\begin{bmatrix}
J_1&&\\
&\ddots&\\
&&J_s
\end{bmatrix}=J
$$
【微观】其中$J_i$ 是一个块：
$$
J_i=\begin{bmatrix}
\lambda_i&1&&&\\
&\ddots & \ddots&&\\
&& \ddots&1\\
&& &\lambda_i
\end{bmatrix}
$$
中文描述，对于整体，就是一些Jordan块在矩阵的对角线上（还记得矩阵分块不？就是这个矩阵块），但是每个块里也有特殊的规定，就是对角线上是一个特征值，注意是一个，然后剩下的，每个特征值头顶上的元素是1，就这样。
每个Jordan块上有一个特征值，对应一个特征向量。

在判断矩阵相似上我们也有了另一种描述矩阵similar中如果A和B相似，他们共享（share）一个Jordan形式，或者说这个定义才是最优版本。
Jordan形式在微分方程，求矩阵高次幂的时候都非常有用，但在实际计算中Jordan Form一般不被使用，因为计算量大，我们希望使用计算量最小的求解方法，A slight change对A就可以把A对角化。

经典名言：

> Proved or not,you have caught the central idea of similarity-to make A as simple as possible while preserving its esstntial properties

上面这个可以当做线性代数的至理名言：
***当一个矩阵被搞得非常非常简单的时候，这个简单的矩阵将保持着最基础的性质***
## Conclusion
本文主要介绍了Similar矩阵，距离最后的高潮只差一下了，大家努力吧，明天SVD





