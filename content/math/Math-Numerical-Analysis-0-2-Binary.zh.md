---
title: 【数值分析】0.2 二进制数字
categories:
    - Mathematic
    - Numerical Analysis
tags:
    - 数制
    - 二进制
    - 十进制
toc: true
date: 2018-05-31 06:12:14
---

**Abstract:** 本文介绍二进制数字的相关知识
**Keywords:** 数制，二进制，十进制

<!--more-->
# 二进制数字
世界一片混乱，大家都说自己是受害者，而当人们接受了不对称不完整的信息后会产生极大的错误判断和所谓的民族情绪，个人认为：你看到的都是别人想让你看到的，而你分析出来的才有可能是真实的。
今天研究二进制，我们在《陶哲轩实分析》中只学了自然数的定义就没有继续了，原因是我觉得那个系列写起来太废时间，而且过多的是整理工作，自己的思考比较少，所以就暂时停止了，是继续还是就此打住，我觉得打住的可能性较大。
自然数的定义可以参考：[https://face2ai.com/Math-Analysis-2-0-The-Natural-Numbers/](https://face2ai.com/Math-Analysis-2-0-The-Natural-Numbers/)

数是一个不存在实体的概念，而我们写的1，2，3，只是一种虚拟概念的一种可见的映射，换句话说，这种实体不只有一种，而且只是一个幻影，一个标志，其本身是没有意义的，只是一个标志，注意我说的是1，2，3是数的标志。当然我们也可以用I，II，III的标志。
上面这句迷糊的话想表示的就是数十个虚无的概念，没有实体，我们人类为了表示，记录简单，自己发明了1，2，3这些符号来使数可见。
当然我们说的二进制，也是数的一种标志，00，01，10和1，2，3是一一对应的，每一组对应都表示同一个数。
![](./1.png)
计算机为什么使用二进制这是计算机基础里面研究的，我就不说了，二进制表现如下：
$$
\cdots b_3b_2b_1b_0.b_{-1}b_{-2}\cdots
$$
我们下面将注意力转移到上图的 $f$ 中，也就是如何进行数制转换。
## 十进制转化为二进制
我们分别处理整数和小数。
整数部分的转化，我们用除（以）2取余的方法：
例如将 $(52)_{10}$ 转换成二进制：
$$
52\div2=26\cdots 1\\
26\div2=13\cdots 0\\
13\div2=6\cdots 1\\
6\div2=3\cdots 0\\
3\div2=1\cdots 1\\
1\div2=0\cdots 1\\
$$

所以 $(52)_{10}=(110101)_2$ 这个我记得高中就学过，教材上称之为辗转相除法（够辗转的），其实说白了就是利用了整数除法的性质来解下面的方程
证明：
$$
x_{0_{10}}=a_{m}2^{m}+\cdots+a_{3}2^{3}+a_{2}2^{2}+a_{1}2^{1}+a_{0}2^{0}\\
\text{suppose: }x_{0_{10}}=2\times x_{1_{10}}+y\\
2\times x_{1_{10}}+y_{1_{10}}=a_{m}2^{m}+\cdots+a_{3}2^{3}+a_{2}2^{2}+a_{1}2^{1}+a_{0}2^{0}\\
\text{so: } \\
y_{1_{10}}=a_{0}\\
y_{2_{10}}=a_{1}\\
\vdots\\
y_{m+1_{10}}=a_{m}\\
$$
小数部分道理一样，只是把除以二，变成了除以二分之一，也就是乘以二，下面我们将 $(0.7)_{10}$ 转化为二进制：
$$
0.7\times2=0.4+1\\
0.4\times2=0.8+0\\
0.8\times2=0.6+1\\
0.6\times2=0.2+1\\
0.2\times2=0.4+0\\
0.4\times2=0.8+0\\
\vdots\\
$$

我们就得到了一个循环小数 $0.101100110\cdots$ 表示成传统形式就是 $0.1\overline{0110}$ 备注，有些时候渲染成htnl会偏移，横线位于 $0110$ 上方。
## 二进制转化为十进制
二进制转十进制就更简单了，对于有限位数，就算乘法和加法就行，但是对于有循环的部分我们就需要数学技巧了。
整数比较简单，我们只举个栗子，不做特殊证明，$(10101)_2$ 转化成十进制：

$$
1\times 2^4+0\times 2^3+1\times 2^2+0\times 2^1+1\times 2^0=21_{10}
$$

小数部分如果是有限的，只需要把上面的基换成 $\frac{1}{2}$ 即可，这里就省略了，但是对于循环小数，我们来点数学技巧，举个例子 $0.\overline{1011}$ (横线在1011上)：

$$
x_{10}=0.\overline{1011}_2\\
x_{10}\times 2^4=0.\overline{1011}_2\times (2^4)=1011.\overline{1011}_2\\
x_{10}\times2^4-x_{10}=1011_2=11_{10}\\
x_{10}=\frac{11}{15}
$$

一个简单的数学技巧，主要用于小数点后面紧跟着循环体，但是如果小数点后面没有紧跟着循环体怎么办，当然是移位啦，比如  $0.10\overline{101}$ (横线在101上)我们的做法是：

$$
x_{10}=0.10\overline{101}_2\\
x_{10}\times 2^2=10.\overline{101}_2\\
x_{10}\times 2^2-10=0.\overline{101}_2\\
$$

然后用上面的方法处理 $0.\overline{101}$  即可

2进制是计算机的根基，目前计算机都是基于2进制的，但是2进制写起来实在太长，为了简短，我们可以找一个2的幂次，但是和10差不多的基，所以计算机里还有8进制和16进制，这两个是和10最接近的2的幂次进制。16进制比较常用，四位2进制就是一个16进制，四是2的幂次，所以16进制使用较多,2进制只包含两个数字 $0,1$ 对应的十进制就是我们熟悉的 $0\cdots9$ 十六进制则是在 $0\cdots 9$ 的基础上扩展了 $a,b,c,d,e,f$

## 总结
今天研究了二进制，不算研究，就是复习了一下数制之间的转化。





