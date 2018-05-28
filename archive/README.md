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

相比Word里插入数学公式之繁琐，LaTeX可谓简单粗暴。虽然新版Word的公式编辑器效率较为提高，但bug挺多，多年过去仍未成气候。在行内公式的处理，LaTeX会通过计算来达到最优间距，Word里行内公式通过对象插入，需要通过基线对齐、调整每个行内公式的字号来达到相同的行距，普通用户几乎不可能完成。对于大量公式录入，基于代码的LaTeX具有特别的优势，例如输入一个矩阵，<img src="https://latex.codecogs.com/gif.latex?$\LaTeX$" title="$A_{ij}$" />可以定义一个命令函数：
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
然后通过简单调用该命令函数
```$$\repbmatnum{3}{4}{A}$$```
可以得到如下矩阵，

<img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;A_{11}&space;&A_{12}&space;&A_{13}&space;&A_{14}&space;\\&space;A_{21}&space;&A_{22}&space;&A_{23}&space;&A_{24}&space;\\&space;A_{31}&space;&A_{32}&space;&A_{33}&space;&A_{34}&space;\end{bmatrix}" title="$$\begin{bmatrix} A_{11} &A_{12} &A_{13} &A_{14} \\ A_{21} &A_{22} &A_{23} &A_{24} \\ A_{31} &A_{32} &A_{33} &A_{34} \end{bmatrix}$$" />

自行脑补下Word公式编辑器怎么写上述公式。

2. 文本编码之统一

用过Word的修订模式的同学有没有被恶心过，改了几个字，就好像整篇文章被重写过一样。LaTeX文档是纯文本格式，所有文本编辑器都可以打开，即使在Linux命令行环境下也可以通过Vim打开修改。由于这个特性，修改文档的任何地方可以配合版本控制工具追溯和比较。在文本环境下编码，你不会因为某个部分隐藏的标记和设置而苦恼；你不会因为各种宏、对象和图片的穿插使用而费劲心思调整格式；当然，你也不会因为doc和docx的兼容性问题而犹豫。

3. 格式处理之便捷

需要换投杂志时，在LaTeX里，仅仅需要引用该杂志提供的`documentclass`，再加上几个参数就能换转换成另一个杂志风格。各种微小的格式设置不用自己逐一修改。图片公式标注完全不需要用户考虑，没有所谓的域代码(事实证明域代码用多了会引起卡顿和难以察觉的问题)来控制题注计数。

[SumatraPDF](https://www.sumatrapdfreader.org/free-pdf-reader.html)在Windows下配合LaTeX引擎进行预览和反向搜索(通过PDF的位置找到LaTeX中编码的位置，从而方便修改)，用户体验极佳。当然如果你不用LaTeX，SumatraPDF也是pdf阅读优秀的工具，打开大文件速度比Adobe家的快不少。各个平台类似的PDF阅读器不一样，Windows下就用[SumatraPDF](https://www.sumatrapdfreader.org/free-pdf-reader.html)，Mac下就用[Skim](https://skim-app.sourceforge.io/)，Linux下就用[Evince](https://wiki.gnome.org/Apps/Evince)。

#### 2.3 [Sublime](https://www.sublimetext.com/)
>效率决定一切

做研究处理文本主要是编写各类程序代码、脚本，另外是数据处理。修改简单的代码、不用调试时，采用文本编辑工具效率最高。Sublime基于C++的实现，有当前最快的运行速度，性能卓越。插件采用Python编写，有完美的生态环境，用户广泛。所有的代码可以在Sublime中预览，插件提供高亮。上文提到的LaTeX可以通过[LaTeXTools](https://github.com/SublimeText/LaTeXTools)进行编写、调试、生成PDF，图片和公式都能预览，应该是使用率最高的LaTeX编写工具。

目前类似的优秀编辑器还有Atom、VS Code等等，为什么要推荐Sublime？我们不是程序员，我们只是程序的搬运工。除了程序之外我们还要进行大量数据处理，这时候效率就十分关键。Sublime可以瞬间打开近百兆的文本文件，方便直接查看我们熟知的切线刚度阵。

Sublime另一项技术就是其卓越的搜索和编辑功能，配合列(块)操作可以轻松编辑规律性的文本文件，也支持正则表达式，方便复杂的文本编辑。

#### 2.4 [Git](https://git-scm.com/)/[GitHub](https://github.com)/[Bitbucket](https://bitbucket.org/)/[SourceTree](https://www.sourcetreeapp.com/)
>专注眼前，托管一切

本文最想推荐的就是本小节的版本控制工具。这几个东西的逻辑是这样，Git是分布式版本控制软件，由Linux作者开发，可以单机运行，也可以自行假设服务器运行。但是不是每个人都有能力假设服务器，[GitHub](https://github.com/)和[Bitbucket](https://bitbucket.org/)两个平台就站出来说，你们这些穷人，我来帮你们架设服务器。于是这两个基于Git的版本控制托管网站就产生了，并且给了用户一个页面进行管理。然后我们这些穷人又说了，每次提交更新都要上你们的网站，多麻烦。Bitbucket就说，好人做到底吧，给你一个管理工具，于是免费的[SourceTree](https://www.sourcetreeapp.com/)就出来了。当然Git本来是没有GUI的，命令行操作，功能上和SourceTree一致。Git的功能异常强大，不需要全都掌握，一张图可以解释其操作逻辑
 
<img src="./git_flow.png" width = "420" height = "300" alt="GitFlowFigure" />

#### 2.7 Matlab
>用最少的工具做最多的事情

Matlab 作为简单计算工具用于理论检验。另一方面作为绘制图形工具功能非常强大。所有的曲线图可以用matlab画，通过export setup设置可以指定导出图形的样式，并且保存常用的图形设置，方便重复调用。绘制有限元网格的矢量图，基于OpenGL实现的基本不存在，矢量图工具[Asymptote](http://asymptote.sourceforge.net/)，能够绘制样条曲面，功能强大，但效率不高，效果不佳，常常有错误。Matlab能够绘制有限元网格矢量图的工具，效率和效果都不错。其`Patch`函数十分强大，可以绘制多边形网格，也能给节点或者单元赋予值，从而画出云图。

### 3 编程工具

#### 3.1 [Visual Studio](https://www.visualstudio.com)

对于Windows下编译调试C/C++和Fortran，肯定是Visual Studio。在我有限的经验里，VS的代码静态分析(静态分析是指不编译不运行情况下，分析代码的语法、逻辑来验证代码的规范性和可靠性)性能是最好的。比如类成员函数、成员变量的提示，VS是最迅速最准确的。有些IDE会提示所有成员变量，却很难找到有用的，点名批评一下Mac下的Xcode。C++代码重构也做得最好。VS的调试工具十分强悍，反应迅速，可以修改配置文件来调试复杂的数据结构。对了新版的VS可以支持跨平台的程序编写，也和Clion一样支持CMake部署工具，与时俱进毕竟宇宙第一。

Visual Studio Community 版本免费。

#### 3.3 [Clion](https://www.jetbrains.com/clion/)

在没有Windows的地方，编写C++最好的IDE只能是Clion了，基于CMake的架构，可以方便地编写跨平台的程序。仿真计算为什么要写跨平台的东西？真以为自己是程序员吗？不是，大型问题可以选择超算进行高性能计算，超算只支持Linux系统，因此跨平台的程序就至关重要。这时如果在Windows下用Clion编写代码，然后通过自带的CMake来部署代码，完成后可以直接在超算上用Cmake部署、编译再运行。

Clion 对于有edu邮箱的同学免费。

#### 3.2 [Intel Compiler](https://software.intel.com/en-us/qualify-for-free-software/student)

市面上编译C/C++和Fortran代码的执行效率最高的就是Intel Compiler了，毕竟天下都是Intel的处理器，自家的编译器肯定开了不少小灶。带有强大的MKL数学库，计算效率毋庸置疑。

Intel Complier 同样对于有edu邮箱的同学免费。

#### 3.5 [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

要在超算上计算，首先要保证自己的代码在Linux下能够正常编译，总不能在超算的远程界面上不断调试。难道因为调试一个程序还要装一个虚拟机或是双系统。Windows 10 上的同学可以激活系统自带的Windows Subsystem for Linux(WSL)。这个系统不是虚拟机，而是完整的Linux环境，基本的界面是个命令行工具，但可以安装X11软件，使得WSL可以运行GUI软件，这样所有Linux下的GUI软件都可以在Windows下运行，效果和原生应用一样。

以上工具皆免费，说了这么多目的为了同学们能不假思索地选择效率最高的工具，希望能有帮助。
