
原文链接：[Eike Ziller](http://blog.qt.digia.com/blog/author/eike/) - [Qt Creator 2.8 RC released](http://blog.qt.digia.com/blog/2013/06/28/qt-creator-2-8-rc-released/)

Qt Creator 2.8发布候选版发布啦

今天，我们自豪的介绍Qt Creator 2.8发布候选版。在已经公布的2.8测试版的特性上，这次的发布候选版包含了大量的缺陷修复，不但有对2.8系列之前已经可用的功能的，也有对新特性的。

这个发布候选版是**您**为我们提供最终反馈的机会，所以请从下面的[链接](http://blog.qt.digia.com/blog/2013/06/28/qt-creator-2-8-rc-released/#downloads)下载，尝试一下，并且通过[缺陷追踪器](http://bugreports.qt-project.org/)、[邮件列表](http://lists.qt-project.org/mailman/listinfo/qt-creator)或者IRC(freenode的#qt-creator频道)报告您发现的任何问题。

如果您对Qt Creator 2.8的新特性感兴趣，您应该首先看一下[2.8测试版发布的博客](http://blog.qt.digia.com/blog/2013/05/30/qt-creator-2-8-0-beta-released/)，在那里您会找到我写下的关于许多新特性的事情。

我还没有提及到的一件事情是，我们实验性的添加了对LLDB(OS X)调试的支持，LLVM调试器。这是很重要的，由于苹果公司在OS X中渐渐去掉了对GDB的支持，所以我们需要提供一个不同的解决方案。我们知道现在实现的功能还并不完善，如果能在剩余的关键问题上获得更多的反馈，对我们来说那就再好不过了。您可以测试LLDB调试支持，找到偏好设置 > 构建和运行 > 构建套件(Preferences > Build & Run > Kits)，找到您的构建套件调试器设置，在下拉框中选择LLDB引擎并且设置LLDB的路径(如果您安装了Xcode命令行工具，就是/usr/bin/lldb)。无论是使用苹果的GCC(基于LLVM)，还是使用Clang来编译项目，都可以使用LLDB调试。如果您遇到了问题，请在主任务[QTCREATORBUG-8825](http://bugreports.qt-project.org/browse/QTCREATORBUG-8825)中添加子任务(按紧邻“Sub-tasks”的+按钮)报告。

延伸一点关于我在测试版博文中提到的“QNX得到了许多修复”：现在已经有一个黑莓(BlackBerry)开发环境设置向导了，它可以帮助用户设置他们的开发环境，包括设置NDK路径、注册和创建调试标签等。设备连接处理被重构了，减少了应用程序启动时间，并且现在设置中可以显示连接状态，也提供了手动连接和断开连接的控制。还有许多修复<img src="http://blog.qt.digia.com/wp-includes/images/smilies/icon_biggrin.gif" alt=":D" class="wp-smiley">。

类似地也延伸下关于对Android的支持：亮点是，现在能够在设备上调试和配置QML，也添加了manifest文件的图形编辑器。还有许多修复<img src="http://blog.qt.digia.com/wp-includes/images/smilies/icon_biggrin.gif" alt=":D" class="wp-smiley">。

开源用户可以在Qt项目[Qt Creator 2.8.0发布候选版下载页面](http://download.qt-project.org/development_releases/qtcreator/2.8/2.8.0-rc)下载。

Qt企业版客户请在[客户门户](http://qt.digia.com/Log-in-Customer-Portal/)下载。我们为企业版的软件包添加了一些扩展，是关于Qt Quick的特别用例。更多信息，请查看[Qt企业产品页面](http://qt.digia.com/Product/Qt-Core-Features--Functions/Developer-Tools/)。


