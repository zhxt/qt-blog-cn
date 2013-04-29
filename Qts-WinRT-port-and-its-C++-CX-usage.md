Qt的WinRT移植和它的C++/CX使用

原文链接：[Oliver Wolff](https://blog.qt.digia.com/blog/author/oliverwolff/) - [Qt’s WinRT port and its C++/CX usage](https://blog.qt.digia.com/blog/2013/04/19/qts-winrt-port-and-its-ccx-usage/)

##背景##

在Friedemann做了[关于Qt的Windows Runtime移植的最初介绍](http://blog.qt.digia.com/blog/2013/02/15/port-to-windows-runtime-kick-started/)之后，我想要做一些技术方面和我们移植方面的进一步介绍。

当研究关于与C++有关的Windows Runtime开发(Windows 8商店程序和Windows runtime组件)，您会反复的发现**C++/CX**。Windows C++/CX是微软开发的C++语言的扩展，通过“尽可能的接近现代C++”[(Visual C++ Language Reference (C++/CX))](http://msdn.microsoft.com/en-us/library/windows/apps/hh699871.aspx)，使得为Windows Runtime开发更容易。在某些情况下，这些扩展看起来像C++/CLI结构，但是它们可能有其它的意义或者稍微不同的语法。

第一个吸引眼球的是，C++/CX文档、例子或程序中会有这样的代码：

<pre>
Foo ^foo = ref new Foo();
</pre>

这个^从根本上是一个指针，但是提供了附加的信息：它是用在使用了引用计数的COM对象上，所以内存管理是自动的。“ref new”关键字意思是要创建一个“Ref class”(请看[Type System (C++/CX)](http://msdn.microsoft.com/en-us/library/windows/apps/hh755822)文档中的Ref classes and structs一节)，意思是通过引用(reference)复制它，通过引用计数(reference count)进行内存管理。因此上面那行代码没有什么神奇的；它只是告诉编译器这个对象的内存可以通过引用计数管理，用户不需要自己删除它。

基本上正如C++/CX的名字告诉我们的那样－－它是C++语言的扩展。作为本机非托管代码(native unmanaged code)，它和Qt的工作方式很像。一些人可能会第n次争论是否有必要再重新造轮子，因为很多“问题”事实上都在C++11中解决了(顺便说一下，在上面的例子中auto foo同样也可以工作)，这是由Windows Runtime开发决定的。

##C++/CX在Qt的WinRT移植中的使用##

微软曾在不同的场合(其中包括在2012年Build大会上)表示，一切能用C++/CX完成的，不用扩展也可以实现，两种情况最终都会变成一样的本地代码。因此我们需要决定是要用新东西，还是继续手动内存管理的繁琐方式等。理论上没有什么阻止我们在WinRT移植中使用C++/CX，但是我们尽量避免它们是有原因的。

其中一个，这些扩展可能阻止想要帮助Winows Runtime移植的开发者深入地查看代码。如果您对这个开发环境没有以往的经验，使用新的结构和关键字(还有新代码)可能足够让您立即关掉编辑器了。虽然不使用CX的WinRT代码可能不是特别美观，没有其它东西能像CX那样晦涩了。

另一个问题是Qt Creator的代码模型(目前还)不能处理这些扩展。例如，您不能使用任何^-指针的自动补全。当然了这些会在Qt Creator中修复，可以用的时候会告诉大家，但是此刻我们最先要做的是Qt移植以及基本的Qt Creator集成(构建、调试和开发)。

鉴于以上事实，我们决定不使用这些扩展。尽管如此，如果谁想要帮助移植并且渴望使用CX，他/她可能需要说服我们来贡献代码(当然是在适当的审查之后<img src='http://blog.qt.digia.com/wp-includes/images/smilies/icon_smile.gif' alt=':)' class='wp-smiley' />)。


##不使用C++/CX的问题和挑战##

不使用C++/CX开发Windows Runtime代码带来的主要问题是严重的文档缺乏。虽然MSDN文档对于某些领域已经有了很大的改进，但对于上述主题基本上什么都没有。在这里要感谢Andrew Knight，他在一开始指导我如何进行这方面的开发，并且在我有问题的时候，总能帮助我解决，我想我正在逐步掌握这些内容。为了帮助其他想要参与工作(并把所有的东西写下来)的人，我会在下面介绍一些基础的部分。

###命名空间###

文档中的命名空间和类的CX使用一样，只是增加了“ABI”作为根命名空间(root namespace)。所以对于[StreamSocket](http://msdn.microsoft.com/library/windows/apps/BR226882)，Windows::Networking::Sockets变成了ABI::Windows::Networking::Sockets。另外，您可能需要Microsoft::WRL(并且还有Microsoft::WRL::Wrappers)。WRL是“Windows Runtime C++ Template Library”的缩写，在Windows Runtime应用程序中用于直接COM访问－－但是当您忽略CX(例如创建实例)时，您仍需要它的功能。

###创建实例###

当不使用CX时，大多数类不能被直接访问。取而代之，需要使用接口类(interface class)。这些类名前面被标记了“I”，所以`StreamSocket`变成了`IStreamSocket`。因为这些类是抽象类。您需要创建一个字符串来表示类的classId。

<pre>
HStringReference classId(RuntimeClass_Windows_Networking_Sockets_StreamSockets);
</pre>

这些RuntimeClass_Windows……结构在相关的头文件中定义并且扩展为字符串，例如像“Windows.Networking.Sockets.StreamSocket”。对象实例化的方式依赖于这个类默认是否能被构造。如果能`ActivateInstance`可以用来获得一个您寻找的类型的对象。

<pre>
IStreamSocket *streamSocket = 0;
if (FAILED(ActivateInstance(classId.Get(), &streamSocket)) {
// handle error
}
</pre>

不幸地是，对于StreamSocket在期望一个ComPtr作为参数的情况下，这个便利的函数ActivateInstance失败了。为了避免这个失败，可以绕个远使用RoActivateInstance

<pre>
IInspectable *inspectable = 0;
if (FAILED(RoActivateInstance(classId.Get(), &inspectable)) {
// handle error
}
if (FAILED(inspectable->QueryInterface(IID_PPV_ARGS(&streamSocket)))) {
// handle error
}
</pre>

如果一个类默认是不可构造的，要创建一个实例，它必须使用工厂(factory)。这些工厂通过调用`GetActivationFactory`来获得，传递适当的类Id。一个像这样的类的例子是`HostName：`

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

习惯了Windows开发的人可能已经注意到了，这些都是基于COM的。意思是所有的这些已经存在很久了，并且被广泛的使用。


###调用静态函数###

对于含有静态函数的类，这些函数有一个额外的接口。这些接口用“Statics”标记在“基础”接口名的后面。并且也可以通过`GetActivationFactory`获得。例如一个包含`GetEndpointPairsAsync`的例子是`IDatagramSocketStatics`。

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

`endpointpairoperation`为这个异步函数定义了回调，但是这个问题会在另一篇文章中介绍。这里有趣的部分是，怎样通过调用`GetActivationFactory`填充`datagramSocketStatics`指针和通过`datagramSocketStatics->GetEndpointPairsAsync(……)`实际调用静态函数。


###ComPtr###

有一种使用引用计数的内存管理方式，它不使用CX，它可以通过使用微软提供的智能指针ComPtr来实现。所以
<pre>
IStreamSocket *streamSocket*
</pre>
将变成
<pre>
ComPtr<IStreamSocket> streamSocket.
</pre>
当使用这些时，我们遇到了一些我们不能解释的内存访问错误(但没有进一步研究)，除此之外，Qt Creator不支持带“streamSocket->”的自动补全，但您一定会调用“streamSocket.Get()->”。因此我们决定不使用ComPtr，但继续使用“常规”指针。所有您必须要做的是记住当您完成使用这个指针时尽快调用“Release”。


总之，我们会尽量避免这些扩展，尽管它可能会使代码不美观。如果您想做贡献，欢迎提交包含CX代码的补丁。如果您有进一步的问题和建议，请随时在评论中提出或者加入我们在freenode的#qt-winrt频道。


