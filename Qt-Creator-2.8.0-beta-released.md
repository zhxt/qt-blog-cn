原文链接： [Eike Ziller](http://blog.qt.digia.com/blog/author/eike/) - [Qt Creator 2.8.0 beta released](http://blog.qt.digia.com/blog/2013/05/30/qt-creator-2-8-0-beta-released/)

今天，我们发布了Qt Creator 2.8测试版。感谢这为这个版本贡献的60名个人贡献者，他们带来了大量的新“内容”和很多很多的bug修复。

这里很难一一覆盖到，像以往一样，我重点介绍其中一些：

现在您可以通过Window > Split New Window打开新的编辑器窗口。这将打开一个和主窗口(例如您也可以切分这个窗口)中的编辑器基本相同的新的窗口。打开一个文档将在最后激活的编辑器窗口中打开一个编辑器。自此以来，引发了非常多的使用问题，它应该以怎样的方式恰当的运行，您(想要)怎样使用这个功能以及当前的方式下您遇到了什么问题，我们需要您的反馈。所以当您发现一些事情应该以不同的方式运行，请通过报告bug，邮件列表或者IRC联系我们。

Qt Creator中对C++支持得到了很多修复，还有更过重构功能：

- 把函数定义从头文件中移动到实现文件中
- 把一个方法的返回值或‘new’表达式到一个本地变量
- 从超级类中为纯虚方法添加声明和实现(非常感谢Lorenz Haas！)

<img class="alignright size-medium wp-image-35988" src="http://blog.qt.digia.com/wp-content/uploads/2013/05/Screen-Shot-2013-05-30-at-09.56.50-300x191.png" alt="" width="300" height="191" />
很多朋用可能没有注意到Qt Creator 2.7有一个并排比较查看器的实验性实现(需要明确的开启)。现在这个比较查看器默认是开启的并且用于git版本控制操作。您还可以使用Tool > Diff来比较任意两个文件。

Git版本控制集成获得了很多新特性，最值得注意的可能是现在您可以在Qt Creator中使用交互rebase。也添加了更新子模块的支持，继续和中止很多操作，还有更多。感谢 Orgad Shaneh和Petar Perisin为这些部分做的工作。

还要感谢Sergey Shambir，贡献了一个带有高亮，缩进和python类向导的python代码编辑器。

另外，还修复了使用CDB调试时许多数据类型的显示，QNX和Andriod也有很多修复，并且还会有更多。更多细节您可以查看[变更日志](http://qt.gitorious.org/qt-creator/qt-creator/blobs/2.8/dist/changes-2.8.0)，或者下载并尝试。

[下载Qt Creator 2.8测试版](http://download.qt-project.org/development_releases/qtcreator/2.8/2.8.0-beta/)

商业版Qt客户请通过[客户渠道](http://qt.digia.com/Log-in-Customer-Portal/)

请使用[我们的bugtracker](http://bugreports.qt-project.org/)报告bug！

注意：我要提及的一件事，以减少惊奇: 进度信息(Progress information)被移动到了Qt Creator主窗口的右下角，带有一个选项来隐藏详细的进度信息并且用只显示一个概要的进度条来代替。



