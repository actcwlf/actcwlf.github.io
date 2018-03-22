---
layout: post
title:  "0基础包教会|数据分析环境搭建：jupyter配置python & r kernel"
author: "actcwlf"
intro: "一个简便易用的数据分析环境"
---

## 前言
作为一个没有妹子的单身狗，旺盛的精力无处宣泄着实可惜，于是便走上了折腾各种工具的不归路。作为拍脑袋的结果，数据分析是我认为最为适宜的方向。
我当前主要计划分享一些在数据分析相关的工具上踩过的坑，希望能对诸位读者有所助益。由于学识和眼界都有限，不免会有疏漏不妥之处，欢迎各位读者批评指正。
第一篇为当前（我亲自认证(/▽＼)）最为便利的数据分析环境Jupyter Notebook的环境搭建指南，面向0基础群众。
## 目录（\*部分选读，不影响主要内容）
1. 简介
2. 准备软件包及安装
3. 配置
4. 包管理
5. 进一步了解\*
6. 美化\*
7. 最终成果

## 简介
* 为什么选择 [Jupyter](http://jupyter.org/)

    >The Jupyter Notebook is an open-source web application that allows you to create and share documents that contain live code, equations, visualizations and explanatory text. Uses include: data cleaning and transformation, numerical simulation, statistical modeling, machine learning and much more.

    官网上的介绍非常清晰，就我个人而言，我选择她的原因有
    1. python & r ... 全功能加持
    2. 交互式的编辑界面
    3. 好看
    4. 好看
    5. 好看

* 但是...

    Q:我知道Jupyter很好，但是Anaconda IPython IRkernel etc. 都是些什么？我需要仔细了解他们吗？

    简单版：不用

    好奇宝宝版：参见进一步了解
## 准备软件包及安装

1. 下载[Anaconda](https://www.continuum.io/downloads)（推荐Python 3.6 64bit版）

2. 下载[R](https://mirrors.tuna.tsinghua.edu.cn/CRAN/) （根据系统选择相应版本）

3. 安装Anaconda，推荐默认配置安装。注意这个路径，自定义与否随意，不过这里要记录下来最终使用的路径。

![anaconda-install](/assets/img/2018-03-22-jupyter-notebook/anaconda-install.PNG)

找到Jupyter Notebook，启动之

![j1](/assets/img/2018-03-22-jupyter-notebook/jupyter-1st.PNG)

出现这个界面表明运行成功

4. 安装R，同样注意这里的路径

![r-install](/assets/img/2018-03-22-jupyter-notebook/r-install.PNG)

找到上述路径下的\bin\r.exe，运行

![r1](/assets/img/2018-03-22-jupyter-notebook/r-1st.PNG)

安装就全部完成了

## 配置

1. jupyter配置启动文件

在安装完成后，我们会发现jupyter默认读取的文件夹并不是我们所希望的，所以第一步的配置就是自定义读取的文件夹。

首先找到jupyter notebook的快捷方式，复制一份命名为jn，右键找到属性

![j2](/assets/img/2018-03-22-jupyter-notebook/jn-2nd.PNG)

在标黄的“目标”最后面添加你想要的路径，不带引号，应用即可。注意下面一栏可以修改，也可以留空，实测没有什么影响。

2. 安装R kernel

jupyter可以支持很多种语言，借助的就是所谓内核（Kernel）的概念，简单理解就是只要安装了某语言的内核，
就可以在jn中使用这种语言（想想都有些小激动），具体的支持列表在[这里](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels)。

具体到R，步骤如下

打开anaconda prompt

![ap](/assets/img/2018-03-22-jupyter-notebook/ap.PNG)

是这个样子的

找到前文提到的r.exe

输入命令
```
cd /d D:\R-language\bin
r
```
cd 是切换路径(change directory)，`/d`选项切换盘符，在同一盘符下可以省略，之后就是具体的目标路径；后面为启动r解释器。

![r-2](/assets/img/2018-03-22-jupyter-notebook/r-2.PNG)

在这里输入
```
install.packages(c('repr', 'IRdisplay', 'evaluate', 'crayon', 'pbdZMQ', 'devtools', 'uuid', 'digest'))
devtools::install_github('IRkernel/IRkernel')
```
安装R Kernel (正式的名称是IRKernel)所需要的文件

之后输入
```
IRkernel::installspec()
```
使得IRKernel在jupyter中生效

![j2](/assets/img/2018-03-22-jupyter-notebook/j3.PNG)

完美！

3. 自定义更多配置\*

经过几次使用，发现好像有一些问题，每次把打开的浏览器关掉，再打开会要求密码；或者说我并不希望每次都自动弹出浏览器。在这些情况下我们可以利用配置文件作自己想要的配置。

打开anaconda prompt

输入下面的代码

```
jupyter notebook --generate-config
```

意思是让jupyter生成配置文件，执行完后找到这个配置文件文件的位置，新建一个同名的.json文件，基本格式为

```
{
  "NotebookApp": {
  }
}
```
在NotebookApp增加你的配置文件，比如我的是

![conf](/assets/img/2018-03-22-jupyter-notebook/conf.PNG)

具体可以自定义的项就在这个.py文件里，读者可以自己发掘

## 包管理

anaconda本身已经包含了许多应用于python的科学计算库，通常直接上手使用即可。如果恰好用到尚未安装的包，可以直接在anaconda prompt中进行管理，使用`conda install package`即可安装

例如安装scipy
```
conda install scipy
```
更多用法，可参阅[这里](http://www.jianshu.com/p/2f3be7781451)

对于在conda中没有的包，也可以使用pip进行安装。

对于R包，并不能在Jupyter的界面中执行安装命令，因此仍然需要在R解释器中利用`install.package()`进行安装，与一般方式无异。

## 进一步了解\*

[IPython](http://ipython.org/)

>IPython provides a rich architecture for interactive computing with:

* A powerful interactive shell.
* A kernel for Jupyter.
* Support for interactive data visualization and use of GUI toolkits.
* Flexible, embeddable interpreters to load into your own projects.
* Easy to use, high performance tools for parallel computing.

简而言之，Ipython提供了一个交互式的python界面，而这种交互方式尤其适用于科学计算

IPython 与 Jupyter

这两者中最先出现的是IPython，随着IPython的发展，其中逐渐增添了一些不仅仅局限于Python语言的组件，例如Notebook etc.
这些组件可以应用到各种语言（例如R）中，因此在IPython 4.0版本，这些组件形成了一个新的项目，即Jupyter，IPython则专注于
交互式的Python界面，以及作为Jupyter的一个内核。

了解更多，可参考IPython主页和[这里](http://www.sohu.com/a/161922708_633700)

anaconda 与 conda

conda 是一个包、依赖和环境管理器，适用于多种语言，其扮演的角色和类似pip于python，npm于javascript，但功能更为强大和全面。详细了解可参阅[这里](https://conda.io/docs/index.html)

anaconda则是以conda作为包管理器，包含了诸多常用python科学计算库的Python发行版，详细了解可参阅[这里](https://www.continuum.io/)

## 美化\*
细心的读者会发现，每次在启动Jupyter Notebook的时候，总是会弹出命令行的界面，这实际上这是启动了一个本地的 Web server，Jupyter就运行在这个Web server上，
浏览器通过访问这个本地的 web server (localhost:8888)就会以网页形式显示出Jupyter的界面，这意味着我们可以利用.css任意自定义Jupyter的界面。
了解网页开发的同学现在就可以动手了(～￣▽￣)～

当然这里不可能让读者再去学网页开发，现在要介绍一款别人造好的轮子[jupyter-themes](https://github.com/dunovank/jupyter-themes)

在anaconda prompt中使用pip进行安装
```
# install/upgrade to latest version
pip install jupyterthemes
```

一些基本命令如下（节选，译自项目Github页面）
```
# 列出现有主题
# onedork | grade3 | oceans16 | chesterish | monokai | solarizedl | solarizedd
jt -l

# 选择主题
jt -t chesterish

# 重置为默认主题
# 注意: 运行命令后需清理浏览器缓存
# 若没有生效，尝试重新启动一个Notebook会话
jt -r


# 将代码字体设置为 'Roboto Mono' 12pt
# (参阅原页面中的字体表)
# 译者注：主题和字体要同时设定
jt -t onedork -f roboto -fs 12
```

## 最终成果
![f](/assets/img/2018-03-22-jupyter-notebook/f.PNG)