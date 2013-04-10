Qt项目新的下载服务需要镜像

原文链接：[Tuukka Turunen](https://blog.qt.digia.com/blog/author/tuturune/) - [Qt Project Needs Mirrors for the New Download Service](http://blog.qt.digia.com/blog/2013/03/28/qt-project-needs-mirrors-for-the-new-download-service/?utm_source=rss&utm_medium=rss&utm_campaign=qt-project-needs-mirrors-for-the-new-download-service)

***目前Qt项目使用内容分发网络(content delivery network)进行版本发布。我们已经开始改进Qt开源版本包的发布，现在镜像配置已经可用了。在正式使用之前，我们需要更多镜像。***

这一次是要切换到基于[MirrorBrain](www.mirrorbrain.org)的系统，远离目前的基于内容分发网络的服务。这项工作由[Daniel Molkentin](https://daniel.molkentin.net/2013/03/27/qt-project-call-for-mirrors/)开始于一段时间之前，现在我们已经可以使用镜像配置了。它和[KDE](http://download.kde.org/)现在使用的很相似。对此我要感谢Danimo和其他来自KDE的朋友，他们的帮助使这一变化成为可能。

***这个系统还没有正式投入使用，我们首先需要足够多的镜像。新的服务下载已经可用，但是系统尚未处理所需的负载。目前我们已经有两个镜像，在新的下载投入使用之前仍需要更多的镜像。***

- 您可以从这里[http://download.qt-project.org](http://download.qt-project.org/)找到新的下载服务
- 怎样成为一个镜像的信息在Qt项目wiki上[http://qt-project.org/wiki/mirror_howto]

新的服务只用于开源内容。所有商业Qt许可持有者使用分开的系统。所以非盈利组织成为Qt项目镜像是完全可以的。

如果您的组织愿意成为一个镜像，请按照[wiki](http://qt-project.org/wiki/mirror_howto)上的步骤。或者如果您了解已经在提供镜像的机构，请您请求他们镜像Qt项目。

我们热切等待新的下载服务上线，它比现在的配置更加灵活。新系统的正式使用也是提供Qt项目新的在线SDK的先决条件。
