# Eclipse-cdt

***

我们都知道高效地编程离不开一款高效的IDE，但是上个十年在ruby等动态语言以及前端技术逐渐流行的时候，社区里掀起了一阵去IDE浪潮，很多人开始诟病IDE启动速度慢，资源占用多，转而去拥抱TextMate，Sublime这类现代化文本编辑器，甚至关于vim和emacs孰优孰劣的争论又开始充斥我们的眼球！我一直很赞成熟练掌握一个跨平台、轻量级的编辑器，这样当我们临时面对一个新的工作环境时不至于束手无策，而且对于像ruby这样的动态语言，IDE可以帮上的忙确实并不比一个现代化文本编辑器多多少，但是这并不是说我们就要从一个极端走向另一个极端。回到静态语言，IDE可以在编译之前就帮程序员进行错误检查，可以精准地索引代码符号，可以准确显示代码元素之间的各种关系，可以支持自动化的重构...，尤其对于较大型的工程，如果没有一款合适的IDE，绝对会极大地影响开发者的工作效率，除非公司本身就不care程序员的开发效率（例如有些公司为了节约固定资产成本给程序员购买低配置的PC；而我所工作的第一个公司甚至一直让程序员使用UltraEdit进行C代码开发）。

IDE所支持的功能可以从代码开发一直到代码测试、构建、调试、发布、部署...，就如何评判一个IDE是否好用，因人而异。我本人认为一个好的IDE应该满足以下几类主要的功能：

- 支持流畅的代码浏览、阅读。
    - IDE要能对程序的符号做分析，建立准确的符号间关系；
    - IDE要能支持各种代码视图，供程序员方便地查看各种代码关系。
    例如函数调用关系，类的引用和继承关系，接口的覆写关系...，而且各种视图的展开和收回需要流畅，符合程序员的习惯。

- 支持快捷高效地代码编辑、开发。
	- 方便快捷地创建目录、文件；
	对目录和文件的创建最好能够支持流畅地全键盘操作；另外支持文件模板设置。
	- 自动化查错；
	可以在代码编写时自动检查错误，以便第一时间发现并修改错误。可以预设代码风格，自动对代码进行格式化。
	- 自动化重构；
	支持通过快捷键自动化完成常用的重构操作。
	- 自动化提示、补全；
	支持对代码符号进行自动化提示，并可以自动补全。另外可以预设代码模板，通过简单几个缩写可以产生常用的代码块。

- 支持灵活方便地代码构建、调试。
	- 由于软件的构建方式可能是多样的，所以IDE应该支持主流的构建配置，此外还得支持对用户个性化构建（用户已有的自动化构建脚本）的扩展。
	- 方便的debug能力，支持各种断点，如条件断点、内存断点，支持各种debug视图。

- 其它辅助功能。
	- 一些针对语言特征的辅助功能；例如针对C\++语言的自动头文件包含，自动宏展开提示等等。
	- 现代IDE还会与时俱进，将功能扩展到代码版本管理，部署等方面；例如支持各种cvs如svn、git；支持将可执行文件部署在docker上运行等等。

- 良好地快捷键支持。
	- 对上面所有的功能，IDE都需要提供方便、流畅的快捷键支持，最终为程序员创建一种沉浸式的体验，可以让程序员把精力专注在代码上，而不是IDE自身带来的偶发复杂度上。

- 跨平台。
	在不同平台上兼容用户使用习惯，各种配置可以导出并在不同平台上导入。

如上所列的feature，根据语言特点不同，IDE的实现难度也不同！由于Java的运行环境和语法相对单纯，所以好用的Java IDE从不匮乏，例如常用的eclipse、intelliJ IDEA等几乎都能做到上述功能！而反观C\++语言，IDE的支持一直不是很理想！由于现代C\++主要用在高性能计算、系统编程、嵌入式开发中，早已不是当年主要被用来做各种windows系统的带UI的工具软件，所以visual studio c\++早已是昨日黄花，难以满足今天对C\++灵活的使用要求了，我们更需要的是一款跨平台的，适应各种使用场景的现代化IDE。

下面对比了个人使用过的一些C\++ IDE；我着重强调了每种IDE的口味，因为我的经验是选择一款IDE其实更多是在选择一种编码风格。

- ** Source Insight **：
准确的说Source Insight并不是一款IDE，只能说是一款代码阅读器。Source Insight对代码开发的支持非常弱，而代码阅读功能倒相对不错，但也仅限于C语言，而且不能有大量的函数指针。Source Insight对OO的支持简直不能让人忍受，一旦有多态，符号跳转就很难准确。Source Insight相对比较轻量，一个源文件再大也能解析，不配置预编译条件也能建立起符号索引关系（不准确而已）。

> Source Insight的口味单一，它喜欢咀嚼传统的C语言工程，不喜欢代码中有太多的函数指针（对它如同鱼刺一样）。它的消化能力很好，文件大点也能吃下，即使有很多预编译条件的不明物体也能尽力吞下消化。适合经常看代码而很少用其写代码的程序员使用！

- ** Visual Studio C\++ **：
如果只在windows下开发，没有跨平台以及交叉编译的需求，可以选择visual studio c\++（后面简称VS）。原生VS对开发效率的支持非常差，一般需要和番茄小助手Visual Assist X结合使用，Visual Assist X为VS提供了代码补全、提示、自动化重构等提高效率的插件功能。由于微软的封闭性，在VS下工作，你的代码构建、调试就必须全被它接管，没有灵活性，但是它debug功能非常强大，我一直觉得微软把心思都用到怎么做好debug上去了，VS的其它方面确实乏善可陈，连类的继承关系视图都不能流畅地显示，非得要人将类名拷贝到一个视图框里面，然后点击鼠标才行，整个操作过程撕裂性极强！据说VS2015做了很大的改善，但是由于本人已经告别windows开发很多年了，没有试用过。

> VS喜欢吃快餐，但又极度挑食，只爱吃按照微软烹调法构建的快餐。它贪快所以易积食，需要经常服用类似Visual Assist X的酶才能较好地吸收营养。适合被绑定在windows下，追求简单强大debug功能的，但是不介意经常使用鼠标，对开发效率没有极致要求的开发人员使用。

- ** Eclipse-cdt **：
Eclipse-cdt是我个人目前最喜欢的C\++ IDE，eclipse-cdt是eclipse针对C\++语言的定制版本，随着针对C\++语言特点进行发展，到目前最新的neon版本，已经是一款非常强大的C\++ IDE（后文中的eclipse代表eclipse-cdt）。首先eclipse是跨平台的，对于linux系统非常友好，在windows下需要cygwin或者minGW之类的仿linux工具链支持，新版本的eclipse为了方便windows下的使用已经兼容了VS工具链。Eclipse是极度灵活的，将所有的配置权交给了使用者，你可以决定每个工程所使用的工具链（支持交叉编译），手动配置头文件查找路径，预编译条件，编译参数等等；如果你会写makefile那么全手工配置一个工程对你来说并不是多难！为了简化配置难度，eclipse支持直接创建一个可执行的工程，或者一个可以自动生成makefile的工程。但是一般情况下，大的C\++工程构建都会有自己的特殊配置，所以掌握手动配置工程基本上是必须的。如果项目已经有自动化构建脚本，eclipse也支持配置外部脚本作为工程构建方式。由于eclipse是开源的，支持以插件扩展，所以很多公司基于eclipse定制了自己的IDE，（例如风河公司针对wxworks开发的workbench，ZTE的KIDE等等），学会了eclipse后再使用这些定制版就一通百通了。但是还是建议大家在[eclipse官网](www.eclipse.org)上跟踪eclipse的新版本，eclipse-cdt最近几年发展很快，很多贴心的功能被加了进来，但是很多程序员还停留在早年对eclipse-cdt的初期印象上！本文后面都是针对eclipse的新版本来谈的，至少是luna之后的版本。
Eclipse最让我觉得舒服的地方在于其强大流畅的代码跳转能力，可以让你流畅地在各种代码关系中徜徉。它对类的引用、继承关系，接口的覆写关系，函数的调用关系等等索引非常准确，并且能以浮现式窗口展现，让你全键盘无缝地在代码中进行跳转。此外eclipse对开发效率的支持也非常好，例如自动添加头文件，重命名文件和改动路径会自动更新所有相关的`#include`路径，对文件模板、代码提示补全、快捷代码块，自动宏展开提示等支持得都很不错。Eclipse支持编辑时自动查错，可以在第一时间发现编译错误。Eclipse支持最基本的自动化重构，例如重命名、提炼变量、提炼方法等等，必须承认在这点上我们对eclipse还有更多的期许！
Eclipse的debug功能一直为人诟病，所以最新几个版本的feature list基本集中在debug相关功能上，但是由于我个人平时很少使用debug，所以对此要求并不高。另外eclipse内置了对git的支持，不过我用惯了命令行，对此也不是很care。我倒希望eclipse后续的开发能把精力主要放在对多工程环境以及自动化重构的支持上。

> Eclipse的口味比较小资，它更喜欢程序员手动烹饪出来的各种私房菜。它喜欢精细的食物，对粗放的食物则往往消化不良（eclipse对大文件支持不好，默认配置是5000行，一旦文件过大，符号解析往往出问题）；有的时候eclipse甚至显得有些洁癖，一旦你的代码风格不统一或者配置有问题，eclipse会出现很多不适症状。Eclipse适合对C\++构建过程比较清楚、对代码风格保持整洁、追求开发效率的程序员使用。

- ** Clion **：
Clion是JetBrains专为C\++出品的IDE，号称 “A power tool for A power language”。我试用了Clion，确切的说目前的现状还是比较蛋疼的。

    - 优点：
    	- 跨平台；
        - 代码提示、补全，快捷键，视图设置等等都更加智能；
        - 更加强大的自动化重构，例如inline函数、extract成员函数、常数，pull up/pull down、修改签名这些功能都有；
    - 缺点：
    	- 资源占用高，可以流畅跑eclipse的资源跑clion却会明显卡顿；
    	- 只支持64位系统；
    	- 构建只支持cmake；

Clion目前是收费的，免费版可以试用30天。

> Clion对就餐环境档次要求很高，对食材的烹饪方式要求级别也比较高，可是它却有点眼大肚子小，由于其新贵出身继承了不少优势，但也正是由于其不够平民化，所以阻碍了其使用范围。Clion口味过于铺张，导致其难以消化太大的工程，否则会让自己负重难行。Clion目前适用于喜欢尝试新鲜事物，相对比较阔绰，没有历史负担的程序员尝鲜使用。对于Clion我们可以跟踪其发展，希望它能够早日接地气！

上面是本人对IDE的一些看法，并分享了我自己使用各种C\++ IDE的切身感受。由于C\++的应用环境比较多样，构建过程比较自由，依赖的外部条件比较多，而且语言也相对复杂，很多语法例如宏、模板特化、函数重载等都会增加IDE的解析难度，所以做好一款C\++ IDE还是很难的，必须得承认目前为止还没有任何一款能够做到java领域的成熟度。但还是得说新版本的eclipse-cdt在各个方面做的还是很不错的，如果能够合理的配置eclipse-cdt，并且熟练掌握它的操作方式，绝对可以帮助你提高C\++的开发效率。

后面的章节分享一下我自己的eclipse-cdt配置，以及一些常用的可以提高效率的操作方式；

## Global configurations

- font: Source Code Pro
- font size: 10
- insert space for tab
- C\++ code style : code template : C\ss++ default header and source file; remove the file comments!
- Code Style : add new formatter : COCK
- Name Style : include guard : UUID
	- Test file name format : TestMyClass.cpp
- Organize Includes:
	- ban `Allow reordering of includes`
- Editor-> Folding : ban `Enable folding when opening a new editor`
- Editor->Syntax Coloring->Macro reference : to red, bold
- Editor->Templates : add `cn` for class name : `${file_base}::`
- Editor->File Types : add `*.tcc` for parsing by `C++ header file`

## Project configurations
- new project
- import project
- project name
- include path
- c++11 support
- outer compile

## operations

- open file
- find resource
- find reference
- method invoke
- jump to defination
- ctrl + H
- new folder / file
- class inheritance
- function override
- rename class
- rename file/ move folder
- add include
- copy line ， move line
- comment
- recent files
- switch view
- format code
- rebuild index
- macro spread