Qt 5.0.2发布了

原文链接：[Tuukka Turunen](http://blog.qt.digia.com/blog/author/tuturune/) - [Qt 5.0.2 Released](http://blog.qt.digia.com/blog/2013/04/10/qt-5-0-2-released/)

今天我们发布了Qt 5.0.2－Qt 5.0系列的第二个补丁版发布。我非常高兴对于Qt 5的兴趣，还有我们添加到Qt 5.0.2发布版中改进的数量。

和Qt 5.0.1相比，Qt 5.0.2带来了超过600项改进，大多数的改进是为了解决Qt用户指出的把程序向Qt 5移植中遇到的问题。作为一个补丁版发布Qt 5.0.2没有引进新功能，但我们增加了新的二进制安装程序，也开启了一些早期Qt 5发布版中曾经有问题的用例。

Qt 5.0.2中的亮点包括：

- 新的二进制安装包－带ANGLE的VS2012和带OpenGL的VS2010(给不使用ANGLE的朋友)
- 这个发行包中包含Creator 2.7.0(Qt 5.0.1附带Creator 2.6.2)
- 编译Qt时容易的跳过模块配置的可能性
- Qt库现在能正确静态链接了
- 在17个不同的Qt模块中总地超过600项改进

更多详情列在Qt5.0.2的变更日志中，请您看一下每一个模块的变更日志－或者查看最重要的几个：[qtbase](https://qt.gitorious.org/qt/qtbase/blobs/release/dist/changes-5.0.2)、[qtdeclarative](https://qt.gitorious.org/qt/qtdeclarative/blobs/release/dist/changes-5.0.2)、[qtwebkit](http://qt.digia.com/Release-Notes/Webkit-Release-Notes-Qt-502/)和[qtmultimedia](https://qt.gitorious.org/qt/qtmultimedia/blobs/release/dist/changes-5.0.2)，还有[Creator 2.7.0发布声明](http://blog.qt.digia.com/blog/2013/03/21/qt-creator-2-7-0-released/)。

一如既往，Qt 5.0.2保持了和Qt 5.0向前和向后的源码兼容性。我们将继续解决一些小问题并且提升每一个发布版的质量。如果您遇到了问题，请先查看[已知问题页面](http://qt-project.org/wiki/Qt502KnownIssues)，在那里您能够找到常见问题的解决方法。如果您发现了Qt 5先前未知的bug，请您报告到[bugreports.qt-project.org](http://bugreports.qt-project.org/)，以便我们在将来的发布版中改进。如果您拥有商业许可，您也可以通过[客户渠道](http://qt.digia.com/Log-in-Customer-Portal/)联系我们。

现在代码仓库中做了Qt 5.0.2标签，开源用户可以在[qt-project.org/downloads](http://qt-project.org/downloads)下载Qt 5.0.2的源码包和安装程序，商业许可持有者可以通过[客户渠道](http://qt.digia.com/Log-in-Customer-Portal/)来获取。
