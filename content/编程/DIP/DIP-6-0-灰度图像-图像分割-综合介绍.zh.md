---
title: 【数字图像处理】6.0:灰度图像-图像分割 综合介绍
date: 2015-02-05 10:14
categories:
  - DIP
tags:
  - 图像分割
toc: true
---
**Abstract:** 数字图像处理：第38天
**Keywords:** 图像分割
<!--more-->
<font color="00FF00">本文最初发表于csdn，于2018年2月17日迁移至此</font>
## 开篇废话
 废话开始，因为图像锐化中使用到了一些分割中的基础知识，所以为了比较连贯，决定跳过图像修复开始图像分割，分割的目的是为了区分图像中不同的区域或物体，人类视觉可以利用多种模型同时计算，也就是我们平时可以轻易的分辨出餐盘里的肉和青菜，并且可以准确的把肉夹到嘴里，而在灰度图中，信息没有人眼捕捉到的多，灰度图像分割多半依靠区域的灰度变化，产生一系列的算法和应用。
本文作为分割的基本介绍，首先会给出分割的基本知识结构，此结构不唯一，以下为各人观点，非严格定义：
![Center][]
## 分割介绍
分割是将图像分为构成它的子区域或物体，其中有些是我们关注的部分有些是不关注的，由于灰度图像中只保存有灰度信息。所以灰度图像的分割依靠的是灰度的两个基本性质之一，不连续性或相似性。后面将要介绍的算法主要分类为：

1. 基于边缘
2. 基于阈值
3. 基于区域
4. 基于形态学方法
5. 基于模糊理论
6. 基于微分方程
7. 基于人工神经网络
8. 其他方法

其中我们主要介绍基础方法，基于边缘，阈值，和区域的方法。基于形态学的方法和其他方法中将介绍主流算法原理和实现。

## 基础知识
对于去不图像区域R，图像分割将满足下面几点：
![Center 1][]
解释下d和e，分割出来的每个区域都会满足一个不同性质，这也是分割他们依据，相邻的两个区域的分类属性必须不同，否则其必然为一个区域。
灰度图像分割主要依据的是不连续性和相似性，其中边缘检测作为基于边缘的分割方法，其主要依靠的是不连续性，而区域分割方法主要依靠的是相似性。
## 总结
分割是图像分析的关键步骤，是从图像处理过渡到计算机视觉的部分，分割以后，我们对关心的目标进行相关计算，得出我们希望的数据，对背景记性舍弃或者保存，降低图像整体目标的复杂性，好的分割可以提高信噪比，使后续运算结果更加准确，降低识别难度。
待续。。。。。


[Center]: ./20150205094128357.jpg
[Center 1]: ./20150205095906242.png





