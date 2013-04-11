Qt 5版本的Visual Studio Add-In 1.2.1发布了

原文链接：[Tuukka Turunen](http://blog.qt.digia.com/blog/author/tuturune/)-[Visual Studio Add-In 1.2.1 for Qt 5 Released](http://blog.qt.digia.com/blog/2013/04/11/visual-studio-add-in-1-2-1-for-qt-5-released/)

***这是忙碌的一周－今天我们发布了Visual Studio Add-in 1.2.1的Qt 5版本。这是针对在之前发布版中问题的一个主要的补丁修正版。除了修正补丁之外，现在对Qt 5的类还支持Visual Studio 2012可视化调试器(debugger visualizers)。商业版本还支持Qt Quick。***

和以前一样，要使用Visual Studio Add-in至少需要Visual Studio专业版。支持Visual Studio 2012(推荐update 2)、2010和2008。

Visual Studio Add-In 1.2.1包含的亮点：

- Qt Quick项目向导、QML关键字高亮显示、商业版还有QML文件预览
- 支持Qt 5类的Visual Studio 2012可视化调试器
- 在同一计算机上支持Qt 4内联附加件(Add-in)和Qt 5内联附加件的可能性(依次)
- 修正了错误的Qt 5库、模块名和头文件路径

您可以在[变更日志]()中找到Visual Studio Add-in 1.2.1的详细变化列表。

同时使用Qt 5 VS Add-in和Qt 4 VS Add-in

Qt Visual Studio Add-in不允许和Qt 5 Add-in同时运行，如果这样了，将会关闭。然而一次使用Qt 4和Qt 5 Add-in时可能的。您必须使用Visual Studio Add-in管理器来控制您想要加载那个版本。额外需要注意的是使用正确的项目和类向导，因为如果系统中安装了两个版本的Add-in，Qt 4和Qt 5的向导都是可见的。

商业版本支持Qt Quick

Digia为Visual Studio Add-in创建了附加功能，只提供给Qt商业许可持有者。商业版中有新的Qt Quick2 程序项目向导，它可以创建包含QML和C++代码的项目。商业版Add-in也提供了QML文件关键字高亮和新的启动qmlviewer预览特性。

在Qt项目下载的客户渠道得到它

新的Visual Studio Add-In 1.2.1对于商业和开源用户都可用。如果您有有效的商业许可，您可以从[客户渠道](http://qt.digia.com/Log-in-Customer-Portal/)下载新的Visual Studio Add-In。开源版可以从[Qt Project](http://qt-project.org/downloads#qt-other)下载。如果您还不是商业用户，您还想尝试附加的功能，您可以试一下商业版的[免费30天评估版](http://qt.digia.com/Try-Qt-Now/)。

我希望您喜欢用Visual Studio开发Qt 5应用。请您从商业支持或Qt项目邮件列表提供反馈。
