Qt 5.1 Alpha 可用啦

原文链接： [Lars Knoll](http://blog.qt.digia.com/blog/author/lars/) - [Qt 5.1 Alpha Available](http://blog.qt.digia.com/blog/2013/04/08/qt-5-1-alpha-available/)

两周前我们通过把开发代码库合并到稳定分支开始了Qt 5.1周期。从那时起，发布团队就忙于使分支稳定，现在我们有第一组Qt 5.1包可用了。
开源版本在新的下载区(http://download.qt-project.org/development_releases/qt/5.1/)商业用户在[客户渠道](http://qt.digia.com/customerportal)。
这些包只是代码主要给曾经已经使用Qt开发的人员。您可以等在接下来几周内出来的测试版(beta),除非你觉得自己可以编译Qt。

自在去年12月发布Qt 5.0以来发生了很多变化，我们设法在这个Alpha版完成的新东西的数量让我音像非常深刻。我们来简短的看下最重要的新特性。

**Android & iOS**

第一个是，我们在Qt 5.1中增加了对Android和iOS的初步支持。这个版本完全支持这两个平台，您可以立即开始为这两个平台开发。所有qtbase(Qt Core, Gui, Network etc.)
都已实现。Qt Quick在Android上工作的非常好并且支持大多数传感器。但也有一定局限性。Multimedia的某些部分没有完全实现，Qt Quick尚未工作在iOS上。工具也仍在进行中。
不是所有的事情都能在Qt Creator中完成，但大部分已经很好很流畅的工作了。正如去年宣布的那样，Qt 5.2将会完全支持Android和iOS，但是Qt 5.1会为开发人员提供创建
这两个平台完整程序的坚实基础。

**Qt Quick Controls简介**

之后，我们最终拥有了跨平台的Qt Quick组件(controls)。这个模块(((QtQuick Controls(原来叫做Desktop Components)和Qt Quick Layouts)提供随时可用的组件
和布局，您可以使用它构建您的用户界面， 从按钮(buttons)、布局(layouts)、悬浮菜单(over menu)和工具栏(toolbars)开始到对话框(dialogs)和高级导航组件。
当然了，它们拥有和基础系统原生部件类似的外观。目前实现了桌面操作系统的组件。对触控平台的支持将会添加在Qt 5.2中。

**附加组件**

同样添加了几个新的模块。首先我们把Qt Sensors作为附加组件带回来了。这个模块模前支持Android、iOS、BlackBerry和Mer(Sailfish)。一个用于控制串口的模块(Qt SerialPort)
也被添加进来，还有一个X11特性的附加组件(Qt X11Extras)。

最后，我们为现有模块添加了许多其它小的特性。更多详情，请您看一下[Qt 5.1特性列表](http://qt-project.org/wiki/New-Features-in-Qt-5.1)。

从现在开始，我们开始工作于Qt 5.1 beta版，我期望在从现在开始的几周内发布。据此，Qt 5.1 final版期望在夏季开始之前发布。让我们知道你对我们Qt 5.1 alpha版的想法。享受吧！