qbs到达了里程碑0.3

原文链接：[Jörg Bornemann](http://blog.qt.digia.com/blog/author/jbornema/) - [qbs reached mile stone 0.3](http://blog.qt.digia.com/blog/2013/04/16/qbs-reached-mile-stone-0-3/)

Qbs,我们的另一个[编译工具](http://qt-project.org/wiki/qbs)，到达了一个新的里程碑。从去年12月发布上一个版本之后，qbs有了如下改进：

整个基础代码做了重大的调整。原型阶段的实验已被移除。Qt Creator插件API已经稳定。测试套件扩展到覆盖了更多的特性。在我们的内部测试场－－和Qt Creator使用的一样－－当测试设施检测到每次代码仓库中新的变化时，qbs会在Linux、OS X和Windows上进行测试。

添加了对安装您自己构建的产品的支持。要安装你的产品到~/foo/bar，使用
qbs install --install-root ~/foo/bar

项目加载阶段变快了。在我的电脑上，构建Qt Creator 2.7时分别创建makefiles的时间图表看起来像这样：

<table>
  <tr>
    <td></td>
    <td>Linux</td>
    <td>Windows</td>
  </tr>
  <tr>
    <td>qmake -r</td>
    <td>26.284 s</td>
    <td>99.581 s</td>
  </tr>
  <tr>
    <td>qbs resolve</td>
    <td>13.813 s</td>
    <td>5.510 s</td>
  </tr>
 </table>

增加的null builds的运行时间，就是检测您的项目没有任何变化。像现在的Qt Creator 2.7(相同的电脑Windows/Linux双系统)。

<table>
  <tr>
    <td></td>
    <td>Linux</td>
    <td>Windows</td>
  </tr>
  <tr>
    <td>(n)make</td>
    <td>3.228s</td>
    <td>45.199 s</td>
  </tr>
  <tr>
    <td>jom</td>
    <td>n/a</td>
    <td>25.098 s</td>
  </tr>
  <tr>
    <td>qbs</td>
    <td>1.884s</td>
    <td>1.630 s</td>
  </tr>
 </table>

这样的性能源于这个事实，qbs只检查项目源文件的时间戳。它已经从之前的构建中知道了创建文件的时间戳。

这种方式在Windows上获得的性能提升比在Linux上多了很多，是因为获取文件的时间戳是难以置信的慢。

对检测项目设置的支持已经被改进了。改变属性像cpp.defines会被注意到并且引起涉及的产品的重新编译。

最后，但不是不重要，Qt 2.7附带一个实验性的Qbs项目管理插件。它提供了加载和编译qbs项目的支持。

