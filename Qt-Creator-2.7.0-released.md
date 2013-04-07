原文链接：[Qt Creator 2.7.0 released](http://blog.qt.digia.com/blog/2013/03/21/qt-creator-2-7-0-released/)

今天，我们很高兴地宣布Qt Creator 2.7.0发布了，带来了许多的新功能、改进和修复。

Qt Creator中对于C++11的支持有很多改进，像alignof、alignas、noexcept关键字以及花括号初始化和更多有关lambda的修复。如果Qt Creator不能确定您的工具链是否支持C++11或者C++98/03，为了更好的体验现在默认为C++11。还有重构方面的改进，例如为加了Q_PROPERTY的类成员变量快速添加访问(getter)和设置(setter)方法。


代码编辑器中对于QML的支持做了许多对Qt Quick2的改进，Qt Quick Designer中也做了大量的工作，现在可以更好地为Qt Quick 2工作。请注意尽管Qt Creator独立二进制安装包是基于Qt 4的并且没有提供必要的基于Qt Quick 2的外部工具(需要使用Qt 5构建)。目前，您可以自己使用Qt 5编译Qt Creator，或者至少使用Qt 5编译qml2puppet(qt-creator/share/qtcreator/qml/qmlpuppet/qml2puppet)，并且把它放到您的Qt 5安装目录下的qtbase/bin(并且确认您的项目使用这个Qt版本的构建套件(Kit))，或者您还可以等待Qt 5.0.2的安装包，它包含了基于Qt 5编译的Qt Creator。

对于BlackBerry的支持，我们增加了一个新的设置界面，它允许从一个NDK路径简单的创建构建套件(和必要的Qt版本信息以及编译器信息)，并且帮助用户注册和生成开发者证书以及上传程序到设备所需的其它文件。还有定义程序外观和行为的bar descriptor文件编辑器，现在可以在纯XML编辑器和图形编辑器间切换。还有许多其它方面的改进，例如在设备上调试。

对试验性的构建工具[QBS](http://qt-project.org/wiki/qbs)的试验性支持，被添加到了Qt Creator。现在二进制包中已经包含了(相当于预览版)，尽管默认是禁用的。如果要开启它，请打开“Help > About Plugins”(Mac下在“Qt Creator > About Plugins“)，选中QbsProjectManager，并且重新启动Qt Creator，不需要下载安装。如果您不知道哪里有使用QBS的项目，可以试试Qt Creator代码的QBS项目文件:)。如果您想自己构建使用QBS的Qt Creator，您首先要获得它的代码：Qt Creator的git仓库现在把QBS作为子模块，您所需要做的就是在您的git checkout副本的顶层目录中执行"git submodule update –init && qmake -r && make"。

当然这只是我们实际所做改进中的很小一部分，如果在这里列举一下调试、Android、VCS、FakeVim，我这里提到的每个话题都可以单独写出一篇文章。这一次书签部分很有幸地得到了关注，感谢Vasiliy Sorokin:)。如果您想了解这个版本中的更多情况，可以参考我们的[变更日志](http://qt.gitorious.org/qt-creator/qt-creator/blobs/2.7/dist/changes-2.7.0)。


开源版本下载：[Qt Creator下载页面](http://releases.qt-project.org/qtcreator/2.7.0/)(或者[Qt项目下载首页](http://qt-project.org/downloads#qt-creator))

Qt商业版本用户请通过[客户渠道](http://qt.digia.com/Log-in-Customer-Portal/)来获取安装包。

对Madde开发者需要着重指出：Qt Creator 2.7中对Madde的支持已经默认禁用了。大多数功能仍然可以通过“generic Linux“使用。如果您仍然想使用Madde插件，您需要在第一次启动Qt Creator 2.7之前开启它，带“-load Madde”参数执行(这里非常重要，否则您将失去现有的Madde设置，像工具链和Qt版本)之后，然后打开“Help > About Plugins”来开启Madde插件。


对于手动禁用了QmlJSTools插件的朋友的重要信息：在Qt Creator 2.7中， Qt4ProjectManager依赖于它，所以您需要重新开启它才能打开qmake项目。

(译者注：感谢齐亮对本篇博客全文进行了仔细认真修正。)

