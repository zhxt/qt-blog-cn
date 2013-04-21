Qt的WinRT移植和它的C++/CX使用

原文链接：[Oliver Wolff](https://blog.qt.digia.com/blog/author/oliverwolff/) - [Qt’s WinRT port and its C++/CX usage](https://blog.qt.digia.com/blog/2013/04/19/qts-winrt-port-and-its-ccx-usage/)

**背景**

在Friedemann做了[关于Qt的Windows Runtime移植的最初介绍](http://blog.qt.digia.com/blog/2013/02/15/port-to-windows-runtime-kick-started/)之后，我想要做一些技术方面和我们移植方面的进一步介绍。

当研究关于与C++有关的Windows Runtime开发(Windows 8商店程序和Windows runtime组件)，您会反复的发现C++/CX。Windows C++/CX是微软开发的C++/CX是C++语言的扩展，通过“尽可能的接近现代C++”[(Visual C++ Language Reference (C++/CX))](http://msdn.microsoft.com/en-us/library/windows/apps/hh699871.aspx)，使得为Windows Runtime开发更容易。在某些情况下，这些扩展看起来像C++/CLI结构，但是他们可能有其它的意义或者稍微不同的语法。

第一个吸引眼球的是当查看C++/CX文档、例子或程序中像这样的行：

<pre>
Foo ^foo = ref new Foo();
</pre>

这个^从根本上是一个指针，但是提供了附加的信息：它是用在ref-counted COM对象上，所以内存管理是自动的。“ref new”关键字意思是要创建一个“Ref class”(请看Ref classes和[类型系统](http://msdn.microsoft.com/en-us/library/windows/apps/hh755822)(C++/CX)中的结构),意思是他是通过引用(reference)复制，通过引用计数(reference count)进行内存管理。因此上面那行代码没有涉及很多神奇的；它只是告诉编译器这个对象的内存可以通过引用计数管理，用户不需要自己删除它。

根本上正如C++/CX的名字告诉我们的那样－－它是C＋＋语言的扩展。一切原生非托管代码都结束了，很像Qt的工作方式。一些人可能会第n次争论是否有必要再重新造轮子，因为很多“问题”事实上都在C++11中解决了(顺便说一下，在上面的例子中auto foo同样工作)，但是这是为Windows Runtime开发而决定的。

**C++/CX在Qt的WinRT移植中的使用**

微软已经说过，在不同的场合(除了别的之外在2012年Build大会上)，一切能用C++/CX完成的同样也能不用扩展完成， 不管哪种情况，一切都结束了，想原生代码一样。因此我们需要决定我们是否要用新的奇特的东西或者采用手动内存管理的繁琐的方式等。理论上没有什么阻止我们在WinRT移植中使用C++/CX，但是我们避免他们是有原因的。

其中一个，这些扩展可能阻止想要帮助Winows Runtime移植的开发者深入的查看代码。如果您对这个开发环境没有以往的经验，使用新的结构和关键字(除了新代码之外)可能足够让您立即关掉编辑器了。虽然不使用CX的WinRT代码可能不是特别美观，没有使它更难理解的非默认的东西了。

另一个问题是Qt Creator的代码模型(目前还)不能处理这些扩展。例如，您不能使用任何^-指针的自动编译。当然了这些会在Qt Creator中修复，可以时候用的时候会告诉大家，但是此刻我们最先要做的是移植和基本的Qt Creator集成(构建，调试和开发)。

由于这些事实，我们决定我们不使用这些扩展。尽管如此，如果谁想要帮助移植并且渴望使用CX，他/她可能需要说服我们来获得代码(当然是在适当的审查之后<img src='http://blog.qt.digia.com/wp-includes/images/smilies/icon_smile.gif' alt=':)' class='wp-smiley' />)。


**不使用C++/CX的问题和挑战**

不使用C++/CX开发Windows Runtime代码带来的主要问题是严重的缺乏文档。虽然MSDN文档一般可以在某些区域改进，对于这个主题几乎缺乏任何东西。但是感谢Andrew Knight，他给我一些如何使用这些的初始概览并且当我有任何附加的问题时都很有帮助，我想我将掌握这些。为了帮助其他想要一起努力(并把所有的东西写下来)的人，我会在下面介绍一些基础的部分。

*命名空间*

文档中的命名空间和类的CX使用一样，只是增加了“ABI”作为root namespace。所以对于StreamSocket，Windows::Networking::Sockets变成了ABI::Windows::Networking::Sockets。另外，您可能需要Microsoft::WRL(并且还有Microsoft::WRL::Wrappers)。WRL是“Windows Runtime C++ Template Library”的缩写，在Windows Runtime应用程序中用于直接COM访问－－但是当您忽略CX(例如创建实例)时，您仍需要它的功能。

*创建实例*

当不使用CX时，大多数类不能被直接访问。取而代之，需要使用接口类(interface classes)。这些类名前面被标记了“I”，所以StreamSocket变成了IStreamSocket。因为这些类是抽象类。您需要创建一个字符串来表示类的classId。

<pre>
HStringReference classId(RuntimeClass_Windows_Networking_Sockets_StreamSockets);
</pre>

这些RuntimeClass_Windows…结构在相关的头文件中定义并且扩展为字符串，例如像 “Windows.Networking.Sockets.StreamSocket”。对象实例化的方式依赖于这个类默认是否能被构造。如果能，ActivateInstance可以用来获得一个你寻找的类型的对象。

<pre>
IStreamSocket *streamSocket = 0;
if (FAILED(ActivateInstance(classId.Get(), &streamSocket)) {
// handle error
}
</pre>

不幸地，对于StreamSocket在期望一个ComPtr作为参数的情况下,这个便利的函数ActivateInstance失败了。为了避免这个失败，可以绕个远使用RoActivateInstance

<pre>
IInspectable *inspectable = 0;
if (FAILED(RoActivateInstance(classId.Get(), &inspectable)) {
// handle error
}
if (FAILED(inspectable->QueryInterface(IID_PPV_ARGS(&streamSocket)))) {
// handle error
}
</pre>

如果一个类默认是不可构造的，要创建一个实例，它必须使用工厂(factory)。这些工厂通过调用GetActivationFactory来获得，传递适当的类Id。一个像这样的类的例子是HostName：

<pre>
HostName:

IHostNameFactory *hostnameFactory;
HStringReference classId(RuntimeClass_Windows_Networking_HostName);
if (FAILED(GetActivationFactory(classId.Get(), &hostnameFactory))) {
// handle error
}
IHostName *host;
HStringReference hostNameRef(L"http://qt-project.org");
hostnameFactory->CreateHostName(hostNameRef.Get(), &host);
hostnameFactory->Release();
</pre>

习惯了Windows开发的人可能已经注意到了，所有的这些是基于COM的。意思是所有的这些已经存在很久了，并且被广泛的热爱。


*调用静态函数*

对于含有静态函数的类，这些函数有一个额外的接口。这些接口用“Statics”标记在“基础”接口名的后面。并且也可以通过GetActivationFactory获得。例如一个包含GetEndpointPairsAsync的一个例子是IDatagramSocketStatics。

<pre>
GetEndpointPairsAsync for example.

IDatagramSocketStatics *datagramSocketStatics;
GetActivationFactory(HString::MakeReference(RuntimeClass_Windows_Networking_Sockets_DatagramSocket).Get(), &datagramSocketStatics);


IAsyncOperation<IVectorView *> *endpointpairoperation;
HSTRING service;
WindowsCreateString(L"0", 1, &service);
datagramSocketStatics->GetEndpointPairsAsync(host, service, &endpointpairoperation);
datagramSocketStatics->Release();
host->Release();
</pre>

endpointpairoperation为这个异步函数定义了回调函数，但是这个问题会在另一篇文章中介绍。这里有趣的部分是datagramSocketStatics指针怎样被填充通过调用GetActivationFactory和通过datagramSocketStatics->GetEndpointPairsAsync(...)实际调用静态函数。


*ComPtr*

有一种使用引用计数的内存管理方式，它不使用CX，它可以通过使用微软提供的智能指针ComPtr来实现。所以
<pre>
IStreamSocket *streamSocket
</pre>
将变成
<pre>
ComPtr<IStreamSocket> streamSocket.
</pre>
当使用这些时，我们遇到了一些我们不能解释的内存访问错误(但没有进一步研究)，除此之外，Qt Creator不支持带“streamSocket->”的自动补全，但您必须调用“streamSocket.Get()->”。因此我们决定不使用ComPtr，但继续使用“常规”指针。所有您必须做的是记住当你完成使用这个指针式尽快调用“Release”


总之，我们尝试避免这些扩展尽管它可能会使代码不美观。如果您想做贡献和自在的使用这些，随便的创建包含CX代码的补丁。如果您有进一步的问题和建议，随时在注释中提出或者加入我们在freenode的#qt-winrt频道。


