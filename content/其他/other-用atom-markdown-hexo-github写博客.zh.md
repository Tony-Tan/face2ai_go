---
toc: true
title: 用atom+markdown+hexo+github写博客
categories:
  - Other
date: 2017-08-24 22:24:52
tags:
  - markdown
  - Hexo
  - LaTeX
  - github
---
**Abstract**：本文推荐一些小插件，和小技巧，目的是快速的完成自己的博客，博客的主要目的是传递经验和思想，这就和观赏性网站有了区别，不需要华丽，简洁，清楚的风格更适合技术人员。
**Keywords**：LaTeX，Markdown，Hexo，Atom

<!--more-->

# 用atom markdown hexo github 写博客

## 开篇废话
为啥我们要写博客，因为我们是文化人，我为啥写博客，因为我当年在吃不上饭的时候通过看书和写博客翻身做主了。。所以我认为想要挣钱也好实现人生目标也好，读书，思考和写作是最好的方式，当然这对我来说是不错的一个组合，当然也有高人通过冥想，做梦，请教高手，自已摸索，拿来主义等多种方式获得知识，这些都是好的，只要能学到东西，能够创造出健壮稳定的功能，都是值得肯定的。但是，大家别忘了魁北克那座倒了的桥，当你写的每一行代码，算的每一组数据关乎人命的时候，不要愧对工程师这个称号！

本文推荐一些小插件，和小技巧，目的是快速的完成自己的博客，博客的主要目的是传递经验和思想，这就和观赏性网站有了区别，不需要华丽，简洁，清楚的风格更适合技术人员。

本人主要做一些机器学习算法研究，所以写博客主要是汉字，英文，数学公式，代码，以及不少的图片来解释数据。

本文的目的是介绍一些功能和插件，具体如何写markdown，LaTeX等内容不在本文介绍之内，可以去google出很多详细资料！

用到了atom，以及hexo一些功能来支持

## Atom写作环境
atom是github搞得一个神一个级别的编辑器，编辑器，说实话，vim我用不来，有人说牛人都用vim，我承认，我不是牛人，但是atom好像搞成了一个乐高玩具一样的模式，可以安装众多的插件，或者你可以自己写一些插件。
本文用到的插件包括但不限于：
### markdown-preview-plus
实时预览：
像这样
![](./markdown-preview-plus.png)
以及LaTeX数学公式预览
像这样
![](./latex.png)
从word类软件启蒙的我们对所见即所得的模式产生依赖，看到结果也好，可以及时纠正一些排版问题

### markdown-scroll-sync
同步滚动，就是编辑器和预览能保持一致，这个很方便，就是你写到哪，预览就能生成到哪。这个6666，csdn也有这个功能，非常赞。
### language-markdown
代码增强，让你的代码好看点。。没啥用。。但是看着舒服
### markdown-image-paste
贴图工具，这个是非常好用的功能，如果你输入的图片非常多，markdown可能是你的噩梦，但是这个工具可以减少一些复杂的操作，但具体的要看你的熟练程度，本人写博客一般都不会写特别长，但是喜欢用图片，一幅图胜过一百句话。
### markdown-table-editor
表格，markdown的表格也是一大奇葩，这个可以减轻点尴尬

| 姓名 | 性别 | 年龄 |
|---- |:---:|:---:|
|tony|M|18|
|tan|M|16|
生成上面的图代码是这样的
```
| 姓名 | 性别 | 年龄 |
|---- |:---:|:---:|
|tony|M|18|
|tan|M|16|
```
注意空格。。反正挺尴尬
讲究看吧，咱们是做研究技术的，又不是做美术的。。哈哈
以上是Atom本地的一些功能插件，主要参考[http://www.cnblogs.com/libin-1/p/6638165.html](http://www.cnblogs.com/libin-1/p/6638165.html)的博客
## Markdown & LaTeX
markdown的语法我是通过在csdn写博客的时候掌握的，当时前三天很痛苦，但是学会了你会发现，word类的软件真的很烦，至于如何学习，这个自行Google。再见，不送。。

LaTeX是写数学公式的法宝，可以预览的情况下，简直是神器，hexo环境下配置具体可以参考
 [hexo latex ](http://blog.csdn.net/emptyset110/article/details/50123231)
 具体的也是。。自己Google去吧
图片工具，这个是后补充的，安装
```
npm install https://github.com/CodeFalling/hexo-asset-image --save
```
很重要，不然图片没办法显示
## Git 和 Github
git是啥，程序员都知道，你不知道？那就快去学习吧，哪怕只会clone也是好的，毕竟可以给老板交差，如果你有很多星星。那我要感谢你为人类软件事业做出的杰出贡献。
github是全球最大的同性交友平台，差不多吧，然后可以把hexo弄上去，意外吧，惊喜吧，不用你买服务器，自己搞个域名就可以，wordpress就行qq空间，一直都挺恶心的，但是之前不知道有hexo，现在果断弃暗投明，具体hexo和github怎么组合网上也一大堆，我用的主题来自yilia，感谢他花时间帮助我们这群没有美感的技术们搞了一个还算不错的样子。
## other
其他一些小的修修补补，比如添加目录什么的，都可以通过baidu得到答案，百度搜索，给你的不只是莆田系，还有不少入门知识！





