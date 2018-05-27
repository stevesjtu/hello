## 仿真计算之研究工具
仿真计算中的计算多体动力学是一门古老而新兴的学科，古老是因为理论基本采用了200多年前的分析力学基础，新兴是因为需要结合计算机技术来实现。因其需要推导大量公式和编写繁琐的程序而深受广大同学的喜爱，于是乎有同学因彻夜疯狂调试程序几近走火入魔。为避免大家为科学而献身，有必要在此记录些许以供参考，如有新的建议可以发起`Issues`或者`Pull requests`。

### 1 准备工作
>工欲善其事，必先利其器。

学习新工具在早期需要投入时间，但习惯之后可以腾云驾雾。首先保持电脑干净状态，所谓干净就是删掉360、百度的所有软件，`Windows 10`有自带杀毒软件 `Defender`作为保障。百度网用来测试网速可以，平时就不要用了，珍爱生命。有条件的上 [Google](https://www.google.com/ncr)，没条件的上 [Bing](https://cn.bing.com)。

### 2 日常工具
日常工具不是QQ或微信，是研究工作中日常使用的工具，分为文献、论文写作及公式推导、版本控制、数据处理和绘制科学图形等内容。

#### 2.1 [Mendeley](https://www.mendeley.com/)/[Endnote](https://endnote.com/)
>参考文献是idea的源泉。

大量的文献不能通过文件夹来维护，**一定**要用`Mendeley`或者`Endnote`进行维护。它们都有word的插件进行插入参考文献、修改参考文献格式等便捷的操作。`Endnote`是老牌的文献管理工具，在知名度上高于`Mendeley`。两者都有云同步功能，可以在网页端任何时间地点查看已同步的文献。但`Mendeley`更年轻，账号有社交功能，会推送你的文献中作者的近期发表状况。也可以根据你的文献来自动推荐相关文献。

`Mendeley/Endnote`不是pdf文件管理器，而是文献信息管理器。所以随时更新好每一篇文献的信息，包括作者(弄清姓和名)、杂志名称、发表年月、doi(通过doi号可以自动正确更新以上所有信息)等等。更新后的信息可以用于对本地文献快速检索，并且可以生成\*.bib文件，方便<img src="https://latex.codecogs.com/gif.latex?\inline&space;$\textsc{Bib}\TeX$" title="$\textsc{Bib}\TeX$" />把文献引入<img src="https://latex.codecogs.com/gif.latex?$\LaTeX$" title="$\LaTeX$" />文档。

#### 2.5 [<img src="https://latex.codecogs.com/gif.latex?$\LaTeX$" title="$\LaTeX$" />](https://www.tug.org/texlive/)
>LaTeX是排版工具，MS-Word是字处理软件

一股不正之风经常说LaTeX一定比Word好用，实际的原因是我们学习Word的时候通常采用鼠标乱点法，反正所见即所得，结果实际上Word并没有学好。而LaTeX怎么学习呢？照着模板以葫芦画瓢，模板实现了所有养眼的效果，然后得到了漂亮的文档，于是就产生了一种LaTeX比Word好的假象。Word处理简单文档十分直观，学习曲线平缓。所以任何公司、企业都不会选择用LaTeX作为文档工具，但不幸的是，在学术上，LaTeX还真比Word合适。

我文章投得少，但是知道国外杂志最好选择LaTeX文档，他们的LaTeX模板一般最新的，但Word模板通常年久失修。Word在三个不同平台上没有统一的格式，即使同一个平台不同版本之间也会有冲突。但是LaTeX不管什么平台和版本得出的文档始终是一致的。以下几点是LaTeX适合学术的原因：
1. 数学公式之和谐
相比Word里插入数学公式之繁琐，LaTeX可谓简单粗暴。虽然新版Word的公式编辑器效率较为提高，但bug挺多，多年过去仍未成气候。在行内公式的处理，LaTeX会通过计算来达到最优间距，Word里行内公式通过对象插入，需要通过基线对齐、调整每个行内公式的字号来达到相同的行距，普通用户几乎不可能完成。对于大量公式录入，基于代码的LaTeX具有特别的优势，例如输入一个矩阵<img src="https://latex.codecogs.com/gif.latex?$\LaTeX$" title="$A_{ij}$" />，可以定义一个宏
```
\newcommand{\repbmatnum}[3]{
  \begin{bmatrix}
    \forloop{ct1}{1}{\value{ct1}<#1 \OR \value{ct1}=#1}{
        \forloop{ct2}{1}{\value{ct2}<#2 \OR \value{ct2}=#2}{
            \ifthenelse{\value{ct2}<#2}{#3_{\arabic{ct1}\arabic{ct2}} &}{#3_{\arabic{ct1}\arabic{ct2}}}
        }
        \ifthenelse{\value{ct1}<#1}{\\}{}
    }
  \end{bmatrix}
}
```
然后通过简单调用该宏
```$$\repbmatnum{3}{4}{A}$$```
可以得到如下矩阵，

<img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;A_{11}&space;&A_{12}&space;&A_{13}&space;&A_{14}&space;\\&space;A_{21}&space;&A_{22}&space;&A_{23}&space;&A_{24}&space;\\&space;A_{31}&space;&A_{32}&space;&A_{33}&space;&A_{34}&space;\end{bmatrix}" title="$$\begin{bmatrix} A_{11} &A_{12} &A_{13} &A_{14} \\ A_{21} &A_{22} &A_{23} &A_{24} \\ A_{31} &A_{32} &A_{33} &A_{34} \end{bmatrix}$$" />

自行脑补下Word公式编辑器怎么写上述公式。

2. 文本编码之统一

用过Word的修订模式的同学有没有被恶心过，改了几个字，就好像整篇文章被重写过一样。LaTeX文档是纯文本格式，所有文本编辑器都可以打开，即使在Linux命令行环境下也可以通过Vim打开修改。由于这个特性，修改文档的任何地方可以配合版本控制工具追溯和比较。

3. 格式处理之便捷

SumatrPDF

#### 2.3 Sublime



#### 2.4 Git/Bitbucket

#### 2.6 Engauge

### 3 编程工具

#### 3.1 Visual Studio

宇宙最好IDE名不虚传。在我有限的经验里，VS的代码静态分析(静态分析是指不编译不运行情况下，分析代码的语法、逻辑来验证代码的规范性和可靠性)性能是最好的。

#### 3.3 Clion

#### 3.2 Intel Compiler

#### 3.4 CMake

#### 3.5 Windows Subsystem ---- linux
