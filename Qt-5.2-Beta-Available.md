Qt 5.2测试版可用了

原文链接：[Lars Knoll](http://blog.qt.digia.com/blog/author/lars/)- [Qt 5.2 Beta Available](http://blog.qt.digia.com/blog/2013/10/23/qt-5-2-beta-available/)

我很高兴地宣布Qt 5.2测试版现在可用了。自Qt 5.1以来，发生了很多变化。除了对新平台的支持，我们也增加了大量的新功能并且完成了大量的改进。

###Qt 无处不在

在Qt 5.2中我们引入了产品就绪(production-ready)的Android版和iOS版Qt移植。大量的工作进入到了这两个平台中，这些移植现在扩展了Qt
的多平台承诺，只使用一个框架、Qt，便可以覆盖桌面、嵌入式系统和移动平台。

通过对Android、iOS和BlackBerry 10的完整支持，Qt 5.2是一个针对移动市场的伟大的解决方案，它使用一套基于Qt的移动应用代码。这对现有的Qt用户也是一个很大的优势。它使得把您的现有桌面或嵌入式应用移植到移动平台变得更加快捷和简单，只需要简单的重新编译它。

###增强的内部构建——更强大更灵活

Qt 5.2引入了一个[新的场景图形渲染器](http://blog.qt.digia.com/blog/2013/09/02/new-scene-graph-renderer/)。这个新的渲染器进一步的改进了Qt Quick的图形性能，为应用释放了更多的CPU时间并且更加有效的使用GPU。

Qt Quick内部过去使用的以前的JavaScript引擎，V8，已经被全新的引擎[Qt-specific engine](http://blog.qt.digia.com/blog/2013/04/15/evolution-of-the-qml-engine-part-1/)替换了。这个新的引擎为了QML和Qt Quick用例从零开始设计。它内部直接操作Qt数据类型，避免了许多转换成本。它有一个JIT和一个解释器，极大的扩展了它支持的平台和操作系统范围。这个解释器还允许我们在iOS上使用这个引擎并且遵循iOS应用商店政策。

###新模块和好的东西


- [Qt Bluetooth](http://doc-snapshot.qt-project.org/qt5-stable/qtbluetooth-index.html): 支持使用Bluez 4.x的Linux和BlackBerry
- [Qt NFC](http://doc-snapshot.qt-project.org/qt5-stable/qtnfc-index.html): 支持Blackberry
- [Qt Positioning](http://doc-snapshot.qt-project.org/qt5-stable/qtpositioning-index.html): 支持在所有平台使用NMEA数据，在Linux上使用GeoClue
- [Qt Windows Extras](http://doc-snapshot.qt-project.org/qt5-stable/qtwinextras-index.html): 在Windows上和原生代码集成
- [Qt Mac Extras](http://doc-snapshot.qt-project.org/qt5-stable/qtmacextras-index.html): 在Mac OS X上和原生代码集成
- [Qt Android Extras](http://doc-snapshot.qt-project.org/qt5-stable/qtandroidextras-index.html): 在Android上和原生代码集成
-  通过[QTimeZone](http://doc-snapshot.qt-project.org/qt5-stable/qtimezone.html)和[QCollator](http://doc-snapshot.qt-project.org/qt5-stable/qcollator.html)改进了地区和时区的支持
-  增强了多种Qt Widgets和一个新的[QKeySequenceEdit](http://doc-snapshot.qt-project.org/qt5-stable/qkeysequenceedit.html)类
-  QML[动画](http://doc-snapshot.qt-project.org/qt5-stable/qml-qtquick-animator.html)在主线程高负载不能被阻塞
-  为[Qt Quick Controls](http://doc-snapshot.qt-project.org/qt5-stable/qtquickcontrols-index.html)增加了一些新特性和移动指定控制
-  可访问性(Accessibility)完整支持所有桌面平台，基本支持Android。

Qt 5.2中所有新特性的更多细节列表，请查看Qt项目wiki上[新特性](http://qt-project.org/wiki/New-Features-in-Qt-5.2)页面。

###Qt Creator 3.0

Qt 5.2将和新的Qt Creator发布版:Qt Creator 3.0一起发布。[Qt Creator 3.0测试版](http://blog.qt.digia.com/blog/2013/10/23/qt-creator-3-0-beta-released/)今天也发布了，它是Qt 5.2测试版二进制包的一部分。新的Qt Creator改进了对Android的支持特性，试验性支持iOS，清理了Creator插件API并且改进了对lldb的支持。


Qt 5.2测试版有Windows、Mac和Linux版二进制安装器。开源用户可以从[Qt项目下载区](http://download.qt-project.org/development_releases/qt/5.2/5.2.0-beta1/)获取Qt 5.2测试版，现有Qt企业客户可以从[Qt企业客户门户](http://qt.digia.com/Log-in-Customer-Portal/)获取。

