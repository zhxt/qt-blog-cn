Qt 5.4发布了

原文链接：[Lars Knoll](http://blog.qt.digia.com/blog/author/lars/) - [Qt 5.4 released](http://blog.qt.digia.com/blog/2014/12/10/qt-5-4-released/)


我们很高兴的宣布Qt 5.4今天发布了， 您可以从[qt.io](http://www.qt.io/download/)下载。和Qt 5.4一起， 我们也发布了[Qt Creator 3.3](http://blog.qt.digia.com/?p=40968)， 还为嵌入式Linux和嵌入式Android了更新了Qt设备创建(Qt for device creation)。

让我们从Qt 5.4开始。这次发布的一个主要聚焦领域是围绕Web技术，我们有许多新的东西要在这介绍。


### Web换新的故事

HTML5和Web技术在过去的一年来变得越来越重要。我们花了去年一年为Qt开发一个全新的Web作品; 
[Qt WebEngine](http://doc.qt.io/qt-5/qtwebengine-index.html)模块是我们在Qt中采用Chromium Web engine长期研发项目的成果。Qt 5.4完整支持大多数在用的桌面和嵌入式平台， Qt WebEngine为您提供了易用的API来嵌入Web内容到基于Qt Widgets和Qt Quick的应用中。

新的[Qt WebChannel](http://doc.qt.io/qt-5/qtwebchannel-index.html)模块为QML/C++和HTML/Javascript之间提供了一个简单易用的桥梁。这使创建使用Qt和Web技术的混合应用成为可能。这两方面通过在Web环境中暴露QObjects来通信。这个模块不仅能够和Qt WebEngine良好工作，还支持任何其他支持Web sockets的浏览器引擎。

作为三方组件，Qt 5.4引入了一个叫做[Qt WebView](http://doc.qt.io/qt-5.4/qtwebview-index.html)的新模块的技术预览版。在不需要整个Qt WebEngine或因基础系统的限制不能够使用的情况下，Qt WebView模块提供了更有限的API来嵌入web浏览器作为基础系统的原生浏览器。在Qt 5.4中，Qt WebView模块支持iOS和Android。

连同在Qt 5.3中就引入的[Qt WebSockets](http://doc.qt.io/qt-5/qtwebsockets-index.html)模块一起，Qt现在为许多最新Web技术提供了非常好的支持，这使得和Web内容交互变得很容易。Qt WebEngine和Qt Webview使得嵌入HTML5更加容易。Qt WebChannel在Qt和HTML5之间创建了混合应用必须的通道， Qt WebSockets允许Qt和许多Web服务间的简便通信。

Qt 5.4仍然包含了旧的Qt Webkit模块。Qt Webkit仍然被支持，但是由于我们认为Qt 5.4完成了，所以不会有新功能添加。我们也计划在将来的发布中废除它，因为新的Qt WebEngine提供了我们需要的东西。在大多数用例中，从Qt Webkit向Qt WebEngine的迁移是相当简单的。 如果您正开始一个新的需要Web能力项目，我们建议您使用Qt WebEngine。


### WinRT版Qt | 完善我们的跨平台支持

Qt 5.4的第二个大的新特性是完成了我们的跨平台故事，Qt完整支持[Windows Runtime](http://doc.qt.io/qt-5/winrt-support.html)。Windows Runtime版Qt早在5.3中作为Beta版支持，现在到达了作为Qt一部分的完全支持的状态。使用Qt Windows Runtime版，您可以为Windows应用商店创建应用，包括Windows Phone 8.1或更新版，Windows 8.1或更新版。

这个移植完成了我们跨平台的故事，Qt现在支持了所有相关桌面，嵌入式和移动操作系统。


### 图形更新

Qt 5.4也带来了很多新的特性和改进。焦点之一是围绕着图形。使用Qt 5.4，现在我们为桌面平台引入了更好的高分辨率显示支持，但在Qt 5.4中仍然是是实验性的支持。如果您有兴趣，可以查看概览[文档](http://doc.qt.io/qt-5/highdpi.html)。

因为没有良好的驱动支持，OpenGL在Windows上的支持在一些情况下有些问题。为了解决这个问题，Qt现在有了在应用程序启动时[动态选择OpenGL实现](http://blog.qt.digia.com/blog/2014/11/27/qt-weekly-21-dynamic-opengl-implementation-loading-in-qt-5-4/)的能力。Qt可以在原生OpenGL驱动，ANGLE的OpenGL ES 2.0实现转换到DirectX或纯软件光栅器之间选择。

[Qt Data Visulaization](http://doc.qt.io/QtDataVisualization/index.html)已经更新到1.2版本，包括了附加的特性，像对表面图的立体渲染（volume rendering）和纹理（texture）支持，以及性能改进。 [Qt Chart](http://doc.qt.io/QtCharts/index.html)更新到了2.0版本，包括了更好的Qt 5模块化，二进制包和小幅改进。


[其他图形方面的改进](http://doc.qt.io/QtDataVisualization/index.html)是新的[QOpenGLWidget](http://doc.qt.io/qt-5/qopenglwidget.html)类，替换了旧的来自Qt 4的QGLWidget类，这允许我们废弃了旧的Qt OpenGL模块，所有相关的功能都可以在Qt Gui中找到。[OpenGLContext](http://doc.qt.io/qt-5/qopenglcontext.html)现在能够包装原生上下文。您可以使用新的[QQuickRenderControl](http://doc.qt.io/qt-5/qquickrendercontrol.html)来渲染Qt Quick场景到离屏缓冲区（offscreen buffer）。更多详情请查看[这篇博文](http://blog.qt.digia.com/blog/2014/09/10/qt-weekly-19-qopenglwidget/)。

最终，Qt 5.4包含了一个新的[Qt Canvas3D](http://doc.qt.io/qt-5.4/qtcanvas3d-index.html)模块的技术预览版，为Qt Quick实现了类似WebGL的API。它使得在Qt Quick中使用WebGL的Javascript代码变得非常容易。

在Qt 5.4中有许多我们必须类出来的新东西。在继续之前，请看我们的Qt 5.4亮点视频。


<embed src="http://player.youku.com/player.php/sid/XODQ3NTUwODg4/v.swf" allowFullScreen="true" quality="high" width="480" height="400" align="middle" allowScriptAccess="always" type="application/x-shockwave-flash"></embed>

[搬运版视频链接](http://v.youku.com/v_show/id_XODQ3NTUwODg4.html)


### 其他的新特性

其他大量的[新特性](http://qt-project.org/wiki/New-Features-in-Qt-5.4)也进入到了Qt 5.4中，在本文中，我将只提及它们中的一部分。
 
现在，Qt支持 [低功耗蓝牙（ Bluetooth Low Energy ）](http://doc.qt.io/qt-5/qtbluetooth-le-overview.html)。在Linux平台是使用BlueZ，对于其他平台的支持会在Qt后续版本中引入。低功耗蓝牙使得和许多现代蓝牙设备通信成为可能，例如可穿戴设备。

对于Android，我们现在有了[原生外观](http://blog.qt.digia.com/blog/2014/12/03/native-android-style-in-qt-5-4/)的[Qt Quick控件](http://doc.qt.io/qt-5/qtquick-controls-qmlmodule.html)，还有更小的部署包，和更快的启动速度。对于iOS和Mac OS X，我们支持最新的操作系统版本，XCode 6和需要新的代码签名风格来发布应用到应用商店。我们非常努力的修复了在Mac OS X 10.10上新风格相关的问题。

Qt Qml现在带来了[Qt 状态机](http://doc.qt.io/qt-5/qmlstatemachine.html)的支持，通过导入新的 QtQml.StateMachine，QtCore也增加了新的QtStorageInfo类，为您提供了关于挂载的设备和卷信息。

[Qt Quick控件](http://doc.qt.io/qt-5/qtquick-controls-qmlmodule.html)带来了全新的外观精美的‘平面样式(flat sytle)‘，它可以在所有平台使用。

Qt 5.4也带来了全新版本的Qt Creator，[Qt Creator 3.3](http://doc.qt.io/qtcreator)。关于更新的更多详情，请查看我们的[另一篇博文](http://blog.qt.digia.com/?p=40968)。


### Qt 设备创建(Device creation)

今天，我们也为设备创建发布了新的版本的开发包。

这里介绍下包含在这次发布中的新特性：

现在我们[初步支持](http://blog.qt.digia.com/blog/2014/12/09/multi-process-embedded-systems-with-qt-for-device-creation-and-wayland/)在Wayland上运行Qt，在基于i.MX6的设备上，使用Weston compositor，包括对视频和[Qt WebEngine](http://doc.qt.io/qt-5/qtwebengine-index.html)的支持。

我们增加了新的B2Qt工具模块，很容易从C++和QML访问设备特定的配置，例如显示屏背光，主机名或电源状态。现在正式支持B2Qt Wi-Fi模块，使得可以很容易配置Wi-Fi网络。


除了这些新特性之外，我们也增加了大量改进：

* eAndroid Qt Multimedia插件更新。
    * 嵌入式Android平台的Qt Multitmedia实现被重构了，形成了一个清晰独立的易于维护的插件。

* SD卡格式化向导，为了更简单的部署b2qt镜像
    * 简单的向SD卡写入系统镜像向导
    * 已经集成在Qt Creator中

* BYOS (Build Your Own Stack)改进
    * 为初始化和维护Yocto构建环境改进了脚本： 使用repo工具来维护不同设备的大量的资源库（meta repositories)

* eLinux: i.MX6设备相机支持
    * Qt Quick应用中使用相机所需要的所有必要的GStreamer插件现在都集成在了相应的系统镜像中
    * 增加了MIPI相机支持

在次版本中，我们也添加了新的硬件参考平台，包括低端配置的无GPU的Freescale Vybrid。Qt设备创建支持的完整参考硬件列表可以在这篇[文档](http://doc.qt.io/QtForDeviceCreation/qtee-supported-platforms.html)中找到。


### 不使用OpenGL的Qt Quick

对于我们的嵌入式用户，另一个很棒的新特性是新的[Qt Quick 2D Renderer](http://doc.qt.io/QtQuick2DRenderer/index.html)模块。这个新的商业附加组件在没有OpenGL硬件加速的嵌入式设备上使用Qt Quick。这个新的Qt Quick2DRenderer模块渲染多数的Qt Quick，通过像DirectFB或Direct2D使用纯软件光栅处理或2D硬件加速。这个模块支持除了OpenGL着色器(shaders)和粒子(particles)之外的所有Qt Quick。

这使得在低端设备上创建现代感观的基于Qt Quick的用户界面成为可能。另外，在含有和没有OpenGL的跨设备的设备组合上使用Qt Quick API的能力，极大的减少了您需要编写和维护UI代码的数量。

为了演示Qt Quick 2D Renderer的能力，我们为Qt软件栈添加了Toradex Colibri VF50和VF61设备作为参考硬件，表明我们能够运行在Freescale Vybrid SoCs上。


### LGPL v3简介

和早前声明的一样，Qt 5.4的开源版本也适用与[LGPLv3](http://opensource.org/licenses/lgpl-3.0.html)许可协议。新的许可协议选项允许我们The Qt Company不在商业方面作出妥协的情况下为整个Qt生态系统推出更多增值组件。也有助于保护第三方开发者的自由，免于消费设备锁定的伤害，防止Tivozation(译者注：http://en.wikipedia.org/wiki/Tivoization & https://www.gnu.org/philosophy/open-source-misses-the-point.html)以及其他不合理的使用。

在Qt 5.4中，一些新的模块仅适用于GPL/LGPLv3或者商业许可协议条款。这些模块包括新的Qt WebEngine，Qt WebView的技术预览版和Qt Canvas 3D。Android样式风格只在商业或LGPLv3许可协议下可用。您可以在[这里](http://www.qt.io/licensing/)找到更多详细信息。


### 感谢Qt社区

Qt 5.4增加了大量的新功能和改进。如果没有伟大的为Qt做贡献的伙伴和开发者社区的帮助，其中有些将不会完成，然而他们并不是The Qt Company的员工。

尽管我不能在这提及到每一个人，我仍然要列举几个。感谢我们的Qt服务伙伴KDAB，他们一如既往的是Qt的第二大贡献者，在这次发布中，特别感谢Milian Wolf为Qt WebChannel所做的工作。我也要感谢来自Audiocodes的Orgad Shaneh对Qt Creator的持续帮助和参与，感谢来自Intel的Thiago Macieira的长期参与。我还要感谢来自Ford的Brett Stottlemyer贡献了新的QML状态机框架以及Ivan Komissarov贡献了新的QStorageInfo类。


确定要尝试Qt 5.4，[www.qt.io/download](http://www.qt.io/download). 尽情享用吧！





