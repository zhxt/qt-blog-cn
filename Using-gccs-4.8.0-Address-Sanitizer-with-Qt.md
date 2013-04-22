在Qt中使用gcc 4.8.0的Address Sanitizer

原文链接：[Kai Koehne](Kai Koehne) - [Using gcc’s 4.8.0 Address Sanitizer with Qt](http://blog.qt.digia.com/blog/2013/04/17/using-gccs-4-8-0-address-sanitizer-with-qt/)

gcc 4.8的一个很酷的新特性是内建的“Address Sanitizer”：C/C++的内存错误检测器，例如，如果您访问了已经删除的内存，它会立刻报告。实际上这是一个来自Clang/LLVM的[Google项目](http://code.google.com/p/address-sanitizer/wiki/AddressSanitizer)，对于LLVM用户这可能不足为奇了，但对我来说不是<img src='http://blog.qt.digia.com/wp-includes/images/smilies/icon_smile.gif' alt=':)' class='wp-smiley' />。官方网站上的文档很令人生畏，我在这里讲些怎样更好的使用的要点，特别是在Qt环境中……

**它是怎样工作的？**

它基本上是重写了malloc和free，并且在访问之前做内存检查(详情请看[项目wiki](http://code.google.com/p/address-sanitizer/wiki/AddressSanitizerAlgorithm))。很显然它采用了一种非常高效的方式，因为相比于不做检查执行仅缓慢了2倍！也许在未来某个时候，我们可以在Qt-Project CI系统中开启它，谁知道呢？

警告：这种方式目前只能工作在Linux和Mac上。MinGW很不幸。

**怎样开启它?**

由于它是编译器套件的一部分，开启它很容易：只要在编译器调用中添加-fsanitize=address -fno-omit-frame-pointer，在连接器调用中添加-fsanitize=address。无论怎样，要捕捉内存分配、释放或者被Qt访问的问题，在您的应用程序和Qt中，都需要加上新的编译参数。针对Qt 5.2有一个实验性的补丁使之变得容易：

[https://codereview.qt-project.org/#change,43420](https://codereview.qt-project.org/#change,43420)

因为是一个新特性，它被安排在dev分支(Qt 5.2)。但是您可以cherry-picking它到例如Qt 5.0。然后您在配置Qt时使用-address-sanitizer，为您的程序执行qmake CONFIG+=address_sanitizer。

如果您不想cherry-pick，您也可以手动为qmake设置命令行参数MAKE_CXXFLAGS、QMAKE_CFLAGS和QMAKE_LFLAGS:
这篇是比较困难，分好几次译的。我再改下。
<pre>
$ qmake QMAKE_CXXFLAGS+="-fsanitize=address -fno-omit-frame-pointer" \
QMAKE_CFLAGS+="-fsanitize=address -fno-omit-frame-pointer" \
QMAKE_LFLAGS+="-fsanitize=address"
</pre>

**怎样使用它？**

只需要运行您的程序！如果您遇到了内存问题，它会终止程序的运行，并且向您显示一个带模块名和地址的栈追踪。您需要一个叫做[asan_symbolize.py](https://llvm.org/svn/llvm-project/compiler-rt/trunk/lib/asan/scripts/asan_symbolize.py)的工具来获取符号(symbol)，之后可能会用到c++filt来解析(de-mangle)C++符号。

**演示！**

<pre>
$ mkdir addresssanitizertest

$ echo "
#include <QDebug>
int main(int, char *[]) {
const char *str = QString("Evil!").toLocal8Bit().constData();
qDebug() << str;
}
" > addresssanitizertest/main.cpp

$ cd addresssanitizertest && qmake -project && qmake CONFIG+=address_sanitizer

…

$ ./addresssanitizertest 2>&1 | asan_symbolize.py | c++filt
=================================================================
==32195== ERROR: AddressSanitizer: heap-use-after-free on address 0x600c0000bcd8 at pc 0x4016ce bp 0x7fff7ccd86c0 sp 0x7fff7ccd86b8
READ of size 1 at 0x600c0000bcd8 thread T0
    #0 0x4016cd in QString::fromUtf8(char const*, int) /home/kkoehne/dev/qt/qt-5.1-gcc-4.8.0-64/qtbase/include/QtCore/../../../../qt-5.1/qtbase/src/corelib/tools/qstring.h:478
    #1 0x401b1e in QDebug::operator<<(char const*) /home/kkoehne/dev/qt/qt-5.1-gcc-4.8.0-64/qtbase/include/QtCore/../../../../qt-5.1/qtbase/src/corelib/io/qdebug.h:117
    #2 0x401282 in main /tmp/addresssanitizertest/main.cpp:6 (discriminator 1)
    #3 0x7fac5c1e3a14 in __libc_start_main ??:?
    #4 0x401118 in _start /home/abuild/rpmbuild/BUILD/glibc-2.17/csu/../sysdeps/x86_64/start.S:123
0x600c0000bcd8 is located 24 bytes inside of 64-byte region [0x600c0000bcc0,0x600c0000bd00)
freed by thread T0 here:
    #0 0x7fac5eab9c5a in __interceptor_free _asan_rtl_
    #1 0x7fac5d353e59 in QArrayData::deallocate(QArrayData*, unsigned long, unsigned long) /home/kkoehne/dev/qt/qt-5.1/qtbase/src/corelib/tools/qarraydata.cpp:125 (discriminator 2)
    #2 0x401c21 in QTypedArrayData::deallocate(QArrayData*) /home/kkoehne/dev/qt/qt-5.1-gcc-4.8.0-64/qtbase/include/QtCore/../../../../qt-5.1/qtbase/src/corelib/tools/qarraydata.h:230
    #3 0x401630 in QByteArray::~QByteArray() /home/kkoehne/dev/qt/qt-5.1-gcc-4.8.0-64/qtbase/include/QtCore/../../../../qt-5.1/qtbase/src/corelib/tools/qbytearray.h:396 (discriminator 1)
    #4 0x401231 in main /tmp/addresssanitizertest/main.cpp:5 (discriminator 1)
    #5 0x7fac5c1e3a14 in __libc_start_main ??:?
previously allocated by thread T0 here:
    #0 0x7fac5eab9e7f in __interceptor_realloc _asan_rtl_
    #1 0x7fac5d35944e in QByteArray::reallocData(unsigned int, QFlags) /home/kkoehne/dev/qt/qt-5.1/qtbase/src/corelib/tools/qbytearray.cpp:1472
    #2 0x7fac5d358d05 in QByteArray::resize(int) /home/kkoehne/dev/qt/qt-5.1/qtbase/src/corelib/tools/qbytearray.cpp:1431
    #3 0x7fac5d77e452 in QUtf8::convertFromUnicode(QChar const*, int, QTextCodec::ConverterState*) /home/kkoehne/dev/qt/qt-5.1/qtbase/src/corelib/codecs/qutfcodec.cpp:130
    #4 0x7fac5d780e91 in QUtf8Codec::convertFromUnicode(QChar const*, int, QTextCodec::ConverterState*) const /home/kkoehne/dev/qt/qt-5.1/qtbase/src/corelib/codecs/qutfcodec.cpp:507
    #5 0x7fac5d77a483 in QTextCodec::fromUnicode(QString const&) const /home/kkoehne/dev/qt/qt-5.1/qtbase/src/corelib/codecs/qtextcodec.cpp:807
    #6 0x7fac5d48dd26 in QString::toLocal8Bit() const /home/kkoehne/dev/qt/qt-5.1/qtbase/src/corelib/tools/qstring.cpp:4020
    #7 0x401215 in main /tmp/addresssanitizertest/main.cpp:5
    #8 0x7fac5c1e3a14 in __libc_start_main ??:?
Shadow bytes around the buggy address:
  0x0c01ffff9740: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c01ffff9750: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c01ffff9760: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c01ffff9770: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c01ffff9780: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
=>0x0c01ffff9790: fa fa fa fa fa fa fa fa fd fd fd[fd]fd fd fd fd
  0x0c01ffff97a0: fa fa fa fa fd fd fd fd fd fd fd fa fa fa fa fa
  0x0c01ffff97b0: 00 00 00 00 00 00 00 fa fa fa fa fa 00 00 00 00
  0x0c01ffff97c0: 00 00 00 fa fa fa fa fa 00 00 00 00 00 00 00 fa
  0x0c01ffff97d0: fa fa fa fa fd fd fd fd fd fd fd fa fa fa fa fa
  0x0c01ffff97e0: 00 00 00 00 00 00 01 fa fa fa fa fa 00 00 00 00
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07
  Heap left redzone:     fa
  Heap righ redzone:     fb
  Freed Heap region:     fd
  Stack left redzone:    f1
  Stack mid redzone:     f2
  Stack right redzone:   f3
  Stack partial redzone: f4
  Stack after return:    f5
  Stack use after scope: f8
  Global redzone:        f9
  Global init order:     f6
  Poisoned by user:      f7
  ASan internal:         fe
==32195== ABORTING
</pre>

享受追踪内存问题的乐趣吧！



