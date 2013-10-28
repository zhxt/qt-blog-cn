Qt Creator 3.0测试版发布了

原文链接： [Eike Ziller](http://blog.qt.digia.com/blog/author/eike/) - [Qt Creator 3.0 beta released](http://blog.qt.digia.com/blog/2013/10/23/qt-creator-3-0-beta-released/)

今天，我们和Qt 5.2测试版一起，发布Qt Creator 3.0测试版。

这个版本改进和增加了许多东西，包括：

*改进了对Android的支持：* 在Qt 5.2中，除了修复了许多缺陷之外，我们还增加了对新的部署机制的支持。这将在一个[单独的博文](http://blog.qt.digia.com/blog/2013/10/09/android-deployment-in-qt-5-2/)中详细介绍。

*实验性的支持iOS:* Qt 5.2将完全支持iOS，并且Qt Creator 3.0也增加了对构建、部署以及在iOS模拟器和iOS设备上运行Qt应用的实验性支持。(实验性意思是您必须在帮助>关于插件>设备支持>iOS这里打开这项功能。)

*对‘裸机(bare metal)’设备的实验性支持：* 同样对‘裸机(bare metal)’设备的实验性支持意思是Qt Ctreator需要在设备上运行一个兼容gdb的调试器。非常感谢Tim Sander对此做出的贡献。

对于C++，增加了“对循环优化”和“提取常量作为函数参数”的重构行为，并且现在您可以为单个文件的内部代码模型指定专门的预处理器指令(看在编辑器工具条旁边挨着行号信息的那个小的'#'按钮)。还有一个新的是显示包含文件层级的视图，特别感谢Przemyslaw Gorszkowski，添加了这个特性和许多许多缺陷修复。

还有，应用和编译输出现在支持ANSI色彩，对比查看器(diff viewer)可以在并排(side-by-side)和内嵌(inline)视图之间切换。还有太多其他事情难以在本博文中提及。

[下载单独的Qt Creator 3.0测试版](http://download.qt-project.org/development_releases/qtcreator/3.0/3.0.0-beta/)

[下载Qt 5.2测试版](http://download.qt-project.org/development_releases/qt/5.2/5.2.0-beta1/)(包含Qt Creator)

[Qt 5.2测试版已知问题](http://qt-project.org/wiki/Qt520-beta1-KnownIssues)
