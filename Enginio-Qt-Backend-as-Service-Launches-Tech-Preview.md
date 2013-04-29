Enginio: Qt后端作为一个服务推出了技术预览版

原文链接：[Makkonen Sami](http://blog.qt.digia.com/blog/author/samakkon/) - [Enginio: Qt Backend as a Service Launches Tech Preview](http://blog.qt.digia.com/blog/2013/04/25/enginio-qt-backend-as-a-service-launches-tech-preview/)

您可能已经在[2012年的Qt开发者大会](http://www.youtube.com/watch?v=O_QkohHZ45s)上听说了Enginio，或者可能偶然发现了我们的网站，[http://engin.io](http://engin.io/)。现在我们已经准备好正式开启我们的Enginio技术预览版的大门，欢迎您来测试。我们已经有一些早期尝鲜者，他们提供的宝贵反馈意见，我们已经用于产品开发。

###为什么用Enginio？###

纵观现有的云解决方案，我们发现仍有改进的空间。它们有时很难上手，并且需要某些基础设施或平台的专业知识，大多数情况下，它们没有Qt/C++应用程序接口。使用这些经验，在我们尝试过为各种各样的程序构建后端之后，我们决定创建一个解决方案，它使用基于Qt的直观接口把应用程序和后端云存储连接起来。使用Enginio，开发人员能够专注于创建他们的应用使之视觉愉悦和运行良好，让Enginio来管理后端功能、扩展、安全和性能。

我们的目标是基于Qt的一句箴言－－“使开发者的生活更简单”，所以我们要做的是为开发者提供一个不复杂的、无压力的后端开发体验。所以我们开始创建一个易用并且为Qt应用开发增值的解决方案，与此同时，把不费力的开发特质传递到其它平台。我们希望能够确保这个Qt后端能够为所有人提供增值。 Enginio也将会在商业运作之下，同时提供给Qt的开源和企业用户。对使用商业许可进行开发的Qt企业用户，稍候会为他们提供一些附加的增值特性和功能。

Enginio技术预览版支持：


- 网页版控制面板(配置和管理您的后端的用户界面)
- Schema-less数据存储(存储应用程序数据的地方)
- 安全模型(控制哪些用户访问什么数据的机制)
- 文件支持(在云端保存小的或者大的文件)
- 全文搜索(通过内容搜索存储的数据)
- Qt/QML客户端库(创建应用程序的简便方式)


###怎样开始？###

- 1. 注册一个[Enginio](http://engin.io/)账户

<img class="aligncenter  wp-image-35596" style="border: 1px solid black" src="http://blog.qt.digia.com/wp-content/uploads/2013/04/enginio_signup1-300x198.png" alt="" width="300" height="198" />


- 2. 设置您的新后端

<img class="aligncenter  wp-image-35597" style="border: 1px solid black" src="http://blog.qt.digia.com/wp-content/uploads/2013/04/enginio_setup-300x198.png" alt="" width="300" height="198" />

- 3. 开发您的应用

Qt库的最新发布版可以从Enginio控制面板找到。

<img class="aligncenter size-medium wp-image-35603" style="border: 1px solid black" src="http://blog.qt.digia.com/wp-content/uploads/2013/04/enginio_dashboard-300x244.png" alt="" width="300" height="244" />

共享库和QML扩展插件，像其它Qt项目一样，使用‘qmake && make && make install’构建和安装。

###Qt实例###

I. 在Qt Creator中选择:文件 > 新建文件或工程……创建新的“Qt Gui Application”(File > New File or Project… and create new “Qt Gui Application”)。

II. 在新工程的pro文件中添加：

<pre>
QT += network
win32:CONFIG(debug, debug|release): LIBS += -lenginioclientd
else: LIBS += -lenginioclient
</pre>

III. 在MainWindow.cpp中：

<pre>
// Include Enginio headers
#include <Enginio/Enginio>
 
// Instantiate Enginio Client
// Copy your backend ID and secret from Enginio dashboard
const QString backendId("YOUR_OWN_BACKEND_ID");
const QString backendSecret("YOUR_OWN_BACKEND_SECRET");
EnginioClient *client = new EnginioClient(backendId, backendSecret);
 
// Create new object to backend
EnginioJsonObject banana("objects.fruits");
banana.insert("name", QStringLiteral("Banana"));
banana.insert("price", 1.59);
EnginioObjectOperation *createOp = new EnginioObjectOperation(client);
createOp->create(banana);
createOp->execute(); // Initiates asynchronous operation
 
// Fetch objects from backend to list model
EnginioObjectModel *objectModel = new EnginioObjectModel();
EnginioQueryOperation *queryOp = new EnginioQueryOperation(client);
queryOp->setObjectType("objects.fruits");
queryOp->setModel(objectModel);
queryOp->execute();
</pre>

###QML例子###

I. 在Qt Creator中选择:文件 > 新建文件或工程……创建新的“Qt Quick 2 Application (Built-in Elements)”(File > New File or Project… and create new “Qt Quick 2 Application (Built-in Elements)”)

II. 在main.qml中：

<pre>
import io.engin 1.0 as Enginio
 
// Instantiate Enginio Client
// Copy your backend ID and secret from Enginio dashboard
Enginio.Client {
    id: client
    backendId: "YOUR_OWN_BACKEND_ID"
    backendSecret: "YOUR_OWN_BACKEND_SECRET"
}
 
Enginio.ObjectModel {
    id: objectModel
}
 
Enginio.QueryOperation {
    id: queryOp
    client: client
    model: objectModel // Query results are added to model
    objectTypes: ["objects.fruits"] // Get all fruit objects
}
 
Component.onCompleted: {
    // Create new object to backend
    var banana = {
        objectType: "objects.fruits",
        name: "Banana",
        price: 1.59
    };
    var createOp = client.createObjectOperation();
    createOp.create(banana);
    createOp.execute();
    createOp.finished.connect(function() {
        // Fetch objects from backend to list model
        queryOp.execute();
    });
}
</pre>

构建和您的互联程序就完成了。

我们想邀请更多的朋友来测试和提供反馈。然而请牢记这项服务仍在开发中并且您可能遇到一些漏洞、变更和崩溃。请到[http://engin.io](http://engin.io/)看一下吧。把您的想法告诉我们。

您可以通过[mailus@engin.io](mailus@engin.io)联系到Enginio的开发团队。
