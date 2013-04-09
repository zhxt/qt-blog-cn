Qt 5.1 Alpha版可用啦

原文链接：[Lars Knoll](http://blog.qt.digia.com/blog/author/lars/) - [Qt 5.1 Alpha Available](http://blog.qt.digia.com/blog/2013/04/08/qt-5-1-alpha-available/)

两周以前，我们开始把dev分支合并到stable分支，也就进入了Qt的5.1周期。从那时起，发布团队就忙于使分支稳定，现在已经有第一组Qt 5.1包可用了。开源版本在新的下载区[download.qt-project.org](http://download.qt-project.org/development_releases/qt/5.1/)，商业用户在[客户渠道](http://qt.digia.com/customerportal)。这次只提供了源码包，主要提供给正在使用Qt开发的人员。除非您觉得自己可以编译Qt，您还可以接着等待几周后发布的Beta版。

自去年12月Qt 5.0发布以来发生了很多变化，这个Alpha版实现的新特性数量让我印象非常深刻。我们来简短地看下最重要的新特性。

**Android & iOS**

首先，我们在Qt 5.1中增加了对Android和iOS的初步支持。这个版本完全支持这两个平台，您可以立即开始为这两个平台开发。所有qtbase(Qt Core、Gui、Network等)都已实现。Qt Quick在Android上工作的非常好并且支持大多数传感器。但也有一定局限性。Multimedia的某些部分没有完全实现，Qt Quick尚未工作在iOS上。工具也仍在进行中。并不是一切都能在Qt Creator中完成，但大部分已经很好很流畅的工作了。正如去年宣布的那样，Qt 5.2将会完全支持Android和iOS，但是Qt 5.1会为开发人员提供创建这两个平台完整程序的坚实基础。

**Qt Quick控件(control)简介**

其次，我们最终拥有了跨平台的Qt Quick控件。这个模块((Qt Quick控件(原来叫做Desktop Components)和Qt Quick布局)提供随时可用的控件和布局，您可以使用它构建您的用户界面，从按钮、布局、悬浮菜单和工具栏开始到对话框和高级导航控件。当然了，它们拥有和底层平台的本地窗口部件一样的观感。目前只针对桌面操作系统进行了实现。对触控平台的支持将会在Qt 5.2中添加。

**附加组件**

同样添加了几个新的模块。首先我们把Qt Sensors作为附加组件带回来了。这个模块目前支持Android、iOS、BlackBerry和Mer(Sailfish)。一个用于控制串口的模块(Qt SerialPort)也被添加进来，还有一个X11特性的附加组件(Qt X11Extras)。

最后，我们还为现有模块添加了许多其它小的特性。更多详情，请您看一下[Qt 5.1特性列表](http://qt-project.org/wiki/New-Features-in-Qt-5.1)。

从现在开始，我们开始工作于Qt 5.1 beta版，我期望在从现在开始的几周内发布。然后，Qt 5.1最终版期望在夏季开始之前发布。如果您对我们的Qt 5.1 alpha版的有什么想法，请告诉我们。玩的愉快！
