# 翻译内容：Model　ＰＨＰ　书籍

#　第一部分　语言特性

## 第一章 新的 PHP

PHP语言正在经历一场复兴。PHP在新特性的帮助下正在转变成现代的脚本语言，如命名空间，traits，闭包，并内置操作码缓存。现代的PHP生态系统正在不断发展壮大。PHP开发人员较少依赖整体框架和更小的专用组件。Composer 的依赖管理帮助我们构建PHP应用程序是革命性的进步;它我们从框架的围墙花园中解放，让我们混搭PHP互通组件来定制我们的PHP应用程序。组件的可通用性就离不开社区的标准，标准由PHP框架的 Interop 组提出。 Model PHP 将引导你到新的 PHP，它会告诉你如何构建和部署PHP应用程序通过使用社区标准，最佳实践，可通用性组件。在我们探讨现代PHP之前，了解PHP的起源也是很重要的。PHP是一种解释型的服务器端脚本语言。这意味着你编写PHP代码，将其上传到一个Web服务器，并通过一个解释器执行。PHP是通常用使用Web服务器有Apache或nginx，通过这些服务器来提供动态内容。然而，PHP也可以用来建立功能强大的命令行应用程序（就像bash中，Ruby，Python等语言）。许多PHP开发人员没有意识到这一点，并错过了一个非常令人兴奋的功能，当然，你不是其中之一。PHP开始于 Rasmus Lerdorf 写的CGI脚本的集合用来统计访问到他的网上简历的数量 Lerdorf命名了他的一套CGI脚本为 “个人主页工具”。这种早期的化身，是完全不同于我们今天所知道的PHP。Lerdorf的早期PHP工具不是一个脚本语言，它只提供基本的变量和自动表单变量的工具来解释HTML嵌入语法。1994年至1998年间，PHP经历了多次修改，甚至经历了几次全面的修改。Andi	Gutmans和Zeev Suraski，来自特拉维夫的两个开发人员，联手 Rasmus Lerdorf 将 PHP从一个小集合的CGI工具变换成一个完整的编程语言，更一致的语法和基本支持面向对象的程序设计。他们命名了他们的最终产品PHP3，它发布于1998年后期。新的PHP绰号是从早期的名字中分离出来的，并且它是一个递归缩写 PHP：Hypertext Preprocessor。PHP3的大多数内容都类似于我们今天所知道的PHP的版本。它为各种数据库，协议和API提供了卓越的可扩展性。PHP3的可扩展性吸引了许多新的开发人员使用PHP。到1998年末，PHP3已经安装在全球 10% Web服务器。今天，PHP语言还在不断的快速发展，并且几十个核心团队开发人员来自世界各地。开发实践已经改变了。以往，常见的做法是写一个PHP文件，将其通过 FTP 上传到生产服务器，并希望它能工作。这是一个可怕的开发策略，但它是必要的，因为缺乏
可行的本地开发环境。如今，我们避开FTP并且使用版本控制来代替它。版本控制软件例如 Git 可以帮助维持分支，建立新的分叉，合并代码。本地开发环境与生产服务器的环境是相同的，感谢虚拟化工具，如 Vagrant和配置工具，如 Ansible，Chef，和 Puppet。我们通过 Composer 的依赖管理来维护PHP组件。我们的PHP代码符合 PSR 规范- 由PHP框架的Interop管理社区标准组发布管理。我们通过 PHPUnit 工具进行代码的深度测试。我们在例如 nginx 的web服务器上部署我们的应用程序通过PHP的FastCGI进程管理器。我们通过操作码缓存来提高应用程序的性能。现代PHP包含了许多新的实践不同于你理解的新的PHP。我也高兴地看到，现在PHP有一个正式的规范草案，在2014年之前这是没有的。成熟的编程语言都有一个规范。通俗的说，规范就是一个权威的大纲定义了PHP的所有内容。这个规范会被解析器，解释器和执行PHP代码的开发人员使用。它不是为创建应用程序和网站的开发人员所创建的。一个PHP官方语言规范正变得越来越重要，因为可以为多个相互竞争的PHP引擎提供统一的实现规范。最初的PHP引擎是Zend引擎，一个由 c 语言编写的PHP解释器，并在PHP4引进。Zend引擎是由 RasmusLerdorf ，Andi Gutmans和Zeev Suraski创建。如今，Zend引擎是Zend公司在PHP社区的主要贡献。但是，Facebook的HHVM是第二个主要的PHP引擎。语言规范确保这两个引擎维持基本的兼容性。

## 第二章 PHP 特性
现代PHP语言有许多令人激动的新功能。这些新的特性将会将PHP程序员从早期版本带到新的 ＰＨＰ，他们将是一个不错的惊喜对于那些从其他语言迁移到ＰＨＰ的程序员。这些新功能使PHP语言成为一个功能强大的平台，并为构建Web应用程序和命令行工具提供一个令人愉快的体验。其中一些功能不是必要的，但仍然让我们的生活更轻松。然而某些功能是必不可少的。例如，命名空间，现代PHP的基石标准，使现代PHP开发人员按照自己的想法来实践（例如，自动加载）。我会介绍每个新功能，解释为什么它是有用的，并且告诉你
如何在自己的项目中实现它。

### 命名空间
如果我要你知道现代PHP最重要的特点，那就是命名空间。在PHP5.3.0中增加，命名空间是组织PHP代码到一个虚拟的层次结构的一个重要工具，堪比操作系统的文件系统的目录结构。每个现代化的PHP组件和框架有它自己的全球组织下唯一的组织码，以便它并不冲突，或声明自己，通用类使用其他供应商的名字。命名空间是很重要的，因为他们让我们创造一起工作的沙盒与其他开发人员的代码。这是现代的PHP组件生态系统的基石概念。组件和框架的作者为大量的 PHP 开发者建立和分发代码，他们没有办法知道或控制哪些类的，接口，功能，和常量用于他们自己的代码。此问题也适用于自己的内部项目。如果你为一个项目编写自定义的PHP组件或类，该代码必须与你所依赖的第三方依赖一起工作。正如我早些时候提到的symfony/httpfoundation组件，你的代码中用到其他开发人员的代码可能使用相同的类，接口，功能，或常量名。如果没有命名空间，名称冲突导致PHP运行失败。使用命名空间，你的代码和其他开发人员的代码可以使用相同的类，接口，功能，或常量名
假设你的代码存在下唯一的供应商的名称空间。如果你正在构建一个小小的个人项目中，只有少数的依赖，类名冲突可能不会是一个大问题。但是，当你工作正在开发一个大的项目与众多第三方的依赖的团队中，名称冲突成为一个非常重要的关注。你无法控制哪些类，接口，函数和常量引入你项目依赖的全局命名空间。这就是为什么命名空间在你的代码是中非常重要的。

### 声明
每一个PHP类，接口，功能，不断的在一个命名空间下被创建（或子命名空间）。命名空间是在一个PHP文件在新的一行顶部声明开始<？PHP 的标签之后。 namespace 声明命名空间的，然后一个空格字符，则该空间的名称，然后闭合分号;字符。请记住，命名空间通常被用来建立一个顶级供应商名称。这个命名空间的例子声明了 Oreilly 供应商名称：

 
    <?php
    namespace	Oreilly;

所有的PHP类，接口，功能，或这个命名空间下声明的常量声明存在 Oreilly 的命名空间.如果我们想组织这本书一样来组织代码呢？我们使用一个子名字空间。子命名空间的声明与前面的例子完全一样。唯一不同的是，我们使用 \ 字符来分开命名空间和子名字空间。下面的示例声明名为ModernPHP的一个子名字空间存在于顶级的 Oreilly 的命名空间下：

    <?php
    namespace	Oreilly\ModernPHP;

所有类，接口，功能，和这个命名空间下声明的常量
声明存在于 Oreilly\ModernPHP 子命名空间，并且，在某种程度上，就像这本书。在同一个命名空间或子名字空间中的所有类不需要在同一个 PHP文件中被声明。您可以指定任何PHP文件的顶部一个命名空间或子名字空间，和该文件成为该命名空间或子名字空间的一部分。

### 导入和别名
在我们有命名空间之前，PHP开发人员通过 Zend 风格的类名解决了这个名称冲突问题。这是由Zend普及的一类的命名方案，在其中PHP类名称中使用框架下划线代替文件系统目录分隔符。这个约定完成了两件事情：它保证类名是独一无二的，并且它启用了自动加载的执行，在PHP类利用下划线代替与文件系统的目录分隔符名来确定类文件的路径。

### 全局命名空间
如果你引用一个类，接口，功能，或常量没有命名空间，PHP假定类，接口，方法，或常量存在于当前的命名空间下。如果这假设是错误的，PHP尝试解析类，接口，功能，或常量。如果您需要引用一个另一个命名空间下的类，接口，功能，你必须使用完全合格的PHP类名（命名空间+名）。您可以键入完全合格的PHP类的名称，也可以导入代码到当前命名空间的通过 use 关键字。


## 面向接口编程

学习如何编写一个接口改变了我作为一个PHP程序员的生活，并且将第三方的PHP组件集成到自己的应用极大的提高了我的能力。接口不是一个新功能，但它们是一个重要的功能，你应该知道并且在日常中使用。那么，什么是一个PHP接口？借口就是两个 PHP对象之间的协议让两个对象布相互依赖，但是却可以做到任意一个对象可以做到的事。接口解耦了我们代码的依赖，它可以让我们的代码依赖于任何一个实现了预期的接口的第三方代码。我们不关心
接口的第三方代码实现;我们只关心的第三方代码对接口的实现。让我们假装我刚到美国佛罗里达州迈阿密的阳光PHP开发者大会。我需要一种方式来获得城镇周围的情况，所以我直奔当地有出租车的地方。他们们有一个微小的现代，斯巴鲁旅行车，和（出乎我的意料）布加迪威龙。我知道我需要一种方式来获得城镇周围，而所有三辆车能帮助我做到这一点。但每辆车确实如此不同。在现代是不错的，但我希望我的车有更多的魅力。我没有孩子，所以旅行车有更多的座位超出我的需要。所以我要布加迪。现实情况是，因为他们都有一个共同的特点，我可以驾驶这三款车中任意一辆，并达到预期的期望。每辆车有一个方向盘，油门踏板，制动踏板，和信号灯，并且每辆车都用汽油为燃料。布加迪可能需要更多的油量，但是驱动接口现代车是一样的。因为所有这三辆汽车有着一样的接口，并且我有机会选择我的首选车（如果我们是诚实的，我可能会选择现代）。这与面向对象的PHP是完全相同的概念。如果我写的代码需要一个一个特定的类，我的代是有限制的，因为它只能使用一个类的对象，直到永远。不过，如果我编写一个接口代码，我的代码马上知道如何使用任何对象实现该接口。

## Traits
我的许多PHP开发人员的朋友被新引入PHP5.4.0 中traits 所迷惑。 Traits 表现得像类，但看起来像接口。一个 trait 是部分类的实现（即，常数，属性和方法），可以被混合到一个或多个现有的PHP类。 Traits 有双重责任：他们说类可以做什么（如接口），以及它们提供了模块化执行（如类）。PHP语言采用的是经典的继承模式。这就意味着只能实现单一继承。你可以扩展根类通过不断创造继承并实现新的功能。此被称为继承层次，它是许多编程语言的通用模式。

## Generators
PHP生成器是在PHP5.5.0引入的一个未充分利用的但却有用的功能。我想很多PHP开发人员没有注意到生成器，因为它们的目的不是显而易见的。生成器是简单的迭代器。不同于标准的PHP的迭代器，PHP生成器不要求你实现Iterator接口中的重量级类。相反，生成器计算和产量迭代值。这对应用程序的性能产生深远的影响。思考一下。一个标准的PHP迭代器在内存中迭代，预先计算数据集。这是种方式是低效率的，特别是大而公式化的数据集。这就是为什么我们使用生成器来计算对后续值存取不征用宝贵的内存。


## 闭包

闭包和匿名函数在PHP5.3.0中被引入，这是我的最喜欢和最常用的两个PHP特性。他们听起来吓人（当我第一次接触它们时，至少我是这么认为的），但他们其实很容易理解。他们是每一个PHP开发人员应具备的有用工具。闭包是一个函数，它被创建的时候它和周围状态就都被封装。存在于封闭的内部封装状态，在封闭的之后，原环境不再存在。这是一个很难把握的概念，但一旦你这么做这将是一个改变人生的时刻。匿名函数确实如此，就是没有名字的函数。匿名函数可以被赋值给变量，就像任何其他的PHP对象。但它仍然是一个函数，你可以调用它，并为它传递参数。匿名函数很有用，特别是回调函数。

## Zend	OPcache
字节码缓存不是PHP中的新内容。我们有独立的可选的扩展例如 PHP缓存（APC），eAccelerator，ionCube和XCache。但直到现在这些都没有内置到PHP核心。至于PHP5.5.0，它有自己的内置字节代码缓存，称为Zend OPcache。首先，让我解释什么是字节码缓存以及为什么它非常重要。PHP是一种解释语言。当PHP解释器执行PHP脚本，解析PHP脚本代码，编译PHP代码将转换成一组现有的 Zend Opcodes（机器代码指令），并且执行该字节码。这会发生在每个PHP文件的每个请求中。这是一个很大的开销，尤其是如果PHP必须解析，编译和对于每一个HTTP请求一遍又一遍执行PHP脚本。要是有办法缓存预编译的字节码，就能减少应用程序响应时间，并能减轻系统资源的压力。字节码缓存存储预编译PHP字节码。这意味着PHP解释器不需要读取，解析和编译PHP代码在每次发出请求时。而是PHP解释器可以从内存中读取的字节码预编译，并立即执行。这里可以一的节省大量的时间，并能显着提高应用程序的性能。

## 内置 HTTP 服务器
你可知道，PHP5.4.0有一个内置的Web服务器吗？这是另一个隐藏的宝藏对于那些认为需要 Apache或者nginx来预览他们应用的开发人员。你不应该将其用于生产，但PHP的内置Web服务器是一个完美的本地开发工具。我每一天都在使用PHP的内置Web服务器，不管我写PHP与否。我用它来预览Laravel和Slim Framework应用程序。我使用它与Drupal内容管理框架来建设网站。我还用它来预览静态HTML和CSS。请记住，PHP内置的服务器是Web服务器。它支持 HTTP 请求，可以展现静态的内容和 运行ＰＨＰ文件。这是本地一个很好的方式来编写和预览HTML，无需安装MAMP，WAMP，或者一个重量级的Web服务器。