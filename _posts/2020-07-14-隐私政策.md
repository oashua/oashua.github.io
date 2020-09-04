---
layout:     post
title:      Anaconda+python安装
subtitle:   
date:       2020-09-04
author:     HSH
header-img: img/post-bg-desk.jpg
catalog: true

---

# Anaconda+python安装

为什么装python还要装这个东西？？长话短说，有anaconda可以同时拥有两个以上不同版本的python，还可以方便地装python的库。当然不想装也不强求。

## 1 Anaconda安装

[anaconda官网](https://www.anaconda.com/products/individual)可以直接下载，目前最新版是python3.8，总是追求最新版本并不好。所以我们在[清华镜像站](https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/)找一个附带python版本低一点的(3.6)anaconda：Anaconda3-4.3.0到5.2.0。当然我们也可以下载最新版然后修改python版本或者建立一个python3.6版本的虚拟环境，这些办法的缺点是比较麻烦。

安装时注意改一下安装位置，还有添加到环境变量(add to environment path)一定要勾选。如果没勾选请重新安装或者搜索将anaconda添加到环境变量的[方法](https://blog.csdn.net/Einsam0/article/details/82656088)。

## 2 更换源

更新源的作用类似于：手机自带了google商店，但是由于国内的限制我们正常是不能装里面的软件的，所以就换另外一个国内的软件商店。对于python的库安装是同样的道理，你会发现有些库安装超级慢甚至直接装不上。[anaconda更新源教程](https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/)

## 3 conda基本操作

在命令提示符（cmd）界面或者anaconda软件界面可以实现python版本控制、库安装等。主要需要掌握建立指定python版本的虚拟环境、环境切换、python版本更换、库安装等命令，大家可以自行去探索。

库安装除了conda命令外pip命令也可以，同样需要更新pip的软件源，与anaconda更新源的方法类似。

## 4 开发环境

到此为止python已经安装好了，我们还需要一个写代码的工具。工具有很多，推荐Visual Studio Code、PyCharm、Jupyter notebook等。VS的优点在于支持包括python几乎所有语言代码的编写，还可以高度定制软件的主题颜色，还有很多可以提升效率和使用体验的拓展。pycharm是专为python设计的开发工具，有点类似visual studio之于C、C++、C#。jupyter notebook与前两者的主要区别是在代码的中间可以添加文本公式等作为笔记，梳理自己的思路，还可以保存代码运行的结果。就像这样：

![](https://wx2.sbimg.cn/2020/09/04/6fQxJ.png)

jupyter notebook直接在浏览器中使用，十分方便。使用前需要做修改文件夹根目录等设置。适合小作业的调试，不适合大工程的编写。

后续有问题欢迎大家交流。
