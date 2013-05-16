Qt化的JavaScript

原文链接： [Jörg Bornemann](http://blog.qt.digia.com/blog/author/jbornema/) - [Qtified JavaScript](http://blog.qt.digia.com/blog/2013/05/16/qtified-javascript/)

当写JavaScript代码时，用不了多久我就会想念一些Qt的C++API中可用的函数。一个很简单的例子是**QList::contains**。在JavaScript中，像这样检查一个数组是否含有一个确定的元素：

<pre>
var names = ["Egon", "Peter", "Raymond", "Waldo"];
if (names.indexOf("Waldo") !== -1)
    print("We've found him!");
</pre>

如果我们能够使用*cantains*方式就好了。但是*Array*没有提供。

幸运的是，JavaScript允许我们通过修改对应的原型对象为内建类型(inbuilt types)添加方法。

<pre>
Array.prototype.contains = function(e) {
    return this.indexOf(e) !== -1;
}
if (names.contains("Waldo"))
    print("We've found him!");
</pre>

耶！现在对于所有数组，我们都可以使用*contain*方法了。

但是，当您尝试迭代数组的关键字时，有一个surprise lurking right around the corner(已知的陷阱/已知的埋伏？)。

<pre>
for (var i in names)
    print(i);
</pre>

将会打印：

<pre>
0
1
2
3
contains
</pre>

我知道数组迭代可以通过索引变量完成……但是……附加的关键字是不可预知的并且会有麻烦。

解决这个问题的方法是把*contains*属性标记为non-enumerable。我们可以使用[Object.defineProperty](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Object/defineProperty)函数，它是从JavaScript 1.8.5后可用的。

<pre>
Object.defineProperty(Array.prototype, "contains", {
    value: function(e) { return this.indexOf(e) !== -1; },
    enumerable: false    // This is the default and can be omitted.
})
</pre>

我们给*Object.defineProperty*传递我们想要增强的对象、要添加属性的名字和一个包含我们的新属性的标志描述对象。

*contains*的值是我们显式直接传递给原型的函数。当使用**for (... in ...)**循环时，把描述对象中的*enumerable*属性设置为false会隐藏*contains*。

通过这种方式，我们可以为内建JavaScript类型*数组*和*字符串*创建像Qt一样友好的API。这可以放在一个.js文件中并且在QML/JS或者qbs项目文件中使用。

您觉得怎么样?像这样的API对您的QML代码有帮助么？您最想要哪一个QList或者QString方法？
