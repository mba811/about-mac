# Latex

## MacTex 安装和 LaTex 回顾

# 1. MacTex安装

进入[MacTex官方网站](https://tug.org/mactex/)直接下载pkg安装包进行安装.

# 2. 中英文混合输入

* * *

    \documentclass[UTF8,nofonts]{ctexart}
    \setCJKmainfont{SimSun} % or any font you have.
    \setCJKsansfont{SimHei}
    \setCJKmonofont{FangSong}
    \begin{document}
    文章内容。
    
    Some Chinese fonts should be installed in your system (SimSun, SimHei, FangSong, KaiTi)\end{document}

并使用`XeLaTex`进行排版

或者使用以下方法:

    \documentclass{article}
    \usepackage{CJKutf8}
    
    \begin{document}
    \begin{CJK}{UTF8}{gbsn}
    围棋 (wéiqí)
    \end{CJK}
    hello
    \end{document}

并使用`LaTex`排版

# 3. LaTex语法

* * *

  * `控制序列`, 是以反斜杠\开头, 以第一个空格或非字母 的字符结束的一串文字, 他们并不被输出, 但是他们会影响输出文档的效果
  * 注释, 在Tex的文档中, 以`%`开始,到该行末尾的所有字符, 都会被TeX系统无视, 只作为文档注释, 不显示在正文中.
  * 环境, `/begin`和`/end`两个控制序列和它们之间的部分被称为环境, 其后的大括号被称为环境名
  * 导言区, `\documentclass{article}`与`\begin{document}`之间的部分被称为导言区, 导言区中的控制序列，通常会影响到整个输出文档

## 3.1. 标题作者日期
   
    \documentclass[UTF8,nofonts]{ctexart}
    \setCJKmainfont{SimSun} % or any font you have.
    \setCJKsansfont{SimHei}
    \setCJKmonofont{FangSong}
    \title{你好，world!}  % 标题
    \author{Andrew Liu}  % 作者
    \date{\today}  % 日期
    \begin{document}
    \maketitle  % 显示标题
    hello world
    
    你好, 世界
    
    \end{document}

## 3.2. 目录章节段落

以后省略导言部分, 只保留`\begin{document}`与`end{document}`之间部分.

在文档类`article/ctexart`中, 定义了五个控制序列来调整行文组织结构。他们分别是

  * `\section{·}`
  * `\subsection{·}`
  * `\subsubsection{·}`
  * `\paragraph{·}`
  * `\subparagraph{·}`
    
```
    \begin{document}
    \maketitle  % 显示标题
    \tableofcontents  % 目录, 编译两次产生效果
    
    你好, 世界
    \section{hello world 1}
    how are you
    \subsection{hello world1.1}
    fine! thank you, and you?
    \subsubsection{hello world 1.1.1}
    \paragraph{hello world}
    is the programming method print
    \subparagraph{hello world}
    is also something.
    \subsection{Hello nanjing1.2}
    \paragraph{南京大学} 位于江苏省南京市
    \end{document}
```


## 3.3. 数学公式

> 使用 AMS-LaTeX 提供的数学功能，我们需要在导言区加载amsmath宏包:`\usepackage{amsmath}`

LaTex的数学模式分为两种:

  * inline模式(`$...$`)
  * display模式(`\[ ... \]`)

```
     % 若需要对display模式下公式进行编号, 使用equation
    \begin{equaion}
    …
    \end{equation}
    接下来是一条公式 $E=mc^2$
    接下来是一条display形式的数学公式
    \[ E=mc^2 \]
    下面是带编号的display数学公式
    \begin{equation}
    E=mc^2.
    \end{equation}
```

**根式与分式**

根式用`\sqrt{·}`来表示, 分式用`\frac{·}{·}`来表示（第一个参数为分子, 第二个为分母）
    
    \[ \pm, \times, \div, \cdot, \cap, \cup,
    \geq, \leq, \neq, \approx, \equiv, \sum, \prod, \lim, \int \]
    % 符号分别为加减, 乘, 除, 点乘, 交, 并, 大于等于, 小于等于, 不等于, 约等于, 恒等于, 连加, 连乘, 极限, 积分
    % \limits和\nolimits来强制显式地指定是否压缩上下标
    $ \sum_{i=1}^n i\quad \prod_{i=1}^n $
    $ \sum\limits _{i=1}^n i\quad \prod\limits _{i=1}^n $
    \[ \lim_{x\to0}x^2 \quad \int_a^b x^2 dx \]
    \[ \lim\nolimits _{x\to0}x^2\quad \int\nolimits_a^b x^2 dx \]

**分隔符**
    
    \[ \Bigg(\bigg(\Big(\big((x)\big)\Big)\bigg)\Bigg) \]
    \[ \Bigg[\bigg[\Big[\big[[x]\big]\Big]\bigg]\Bigg] \]
    \[ \Bigg \{\bigg \{\Big \{\big \{\{x\}\big \}\Big \}\bigg \}\Bigg\} \]
    \[ \Bigg\langle\bigg\langle\Big\langle\big\langle\langle x
    \rangle\big\rangle\Big\rangle\bigg\rangle\Bigg\rangle \]
    \[ \Bigg\lvert\bigg\lvert\Big\lvert\big\lvert\lvert x
    \rvert\big\rvert\Big\rvert\bigg\rvert\Bigg\rvert \]
    \[ \Bigg\lVert\bigg\lVert\Big\lVert\big\lVert\lVert x
    \rVert\big\rVert\Big\rVert\bigg\rVert\Bigg\rVert \]

**省略号**

    \[ x_1,x_2,\dots ,x_n\quad 1,2,\cdots ,n\quad
    \vdots\quad \ddots \]

**矩阵**

    \[ \begin{pmatrix} a&b\\c&d \end{pmatrix} \quad \]
    \[ \begin{bmatrix} a&b\\c&d \end{bmatrix} \quad \]
    \[ \begin{Bmatrix} a&b\\c&d \end{Bmatrix} \quad \]
    \[ \begin{vmatrix} a&b\\c&d \end{vmatrix} \quad \]
    \[ \begin{Vmatrix} a&b\\c&d \end{Vmatrix} \]

**分段函数**
    
    \[ y= \begin{cases}
    -x,\quad x\leq 0 \\
    x,\quad x>0
    \end{cases} \]

## 3.4. 图片和表格

**图片**

在Tex源文件同目录下, 放置1.jpg, 使用graphicx宏包提供的\includegraphics命令

    \documentclass{article}
    \usepackage{graphicx}
    \begin{document}
    \includegraphics[width = .8\textwidth]{a.jpg}  % 控制图片大小
    \end{document}

**表格**

    \begin{tabular}{|l|c|r|}
     \hline
    操作系统& 发行版& 编辑器\\
     \hline
    Windows & MikTeX & TexMakerX \\
     \hline
    Unix/Linux & teTeX & Kile \\
     \hline
    Mac OS & MacTeX & TeXShop \\
     \hline
    通用& TeX Live & TeXworks \\
     \hline
    \end{tabular}

## 3.5. 版面设置

**行间距** 设置为1.5倍

    \usepackage{setspace}
    \onehalfspacing

**段间距**

    \addtolength{\parskip}{.4em}  % 在原有的基础上，增加段间距 0.4em

# 4. 相关链接

* * *

  * [一份不太简短的 LATEX 2ε 介绍](http://www.mohu.org/info/lshort-cn.pdf)
  * [一份其实很短的 LaTeX 入门文档](http://liam0205.me/2014/09/08/latex-introduction/)
  * [How do I typeset unicode characters with TexShop?](http://tex.stackexchange.com/questions/111199/how-do-i-typeset-unicode-characters-with-texshop)
  * [MacTex typeset chinese](https://www.google.com/webhp?sourceid=chrome-instant&ion=1&espv=2&es_th=1&ie=UTF-8#es_th=1&q=MacTex%20typeset%20chinese)
  * [MathJax basic tutorial and quick reference](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)
