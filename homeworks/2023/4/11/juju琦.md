# \## 学习链接的作用

1.理解链接器将帮助你构造大型程序。 构造大型程序的程序员经常会遇到由于缺少模块、缺少库或者不兼容的库版本引起的链接器错误。 
除非你理解链接器是如何解析引用、什么是库以及链接器是如何使用库来解析引用的，否则这类错误将令你感到迷惑或挫败。

2.理解链接器将帮助你避免一些危险的编程错误。 
linux链接器解析符号引用时所做的决定可以不动声色地影响你程序的正确性。 在默认情况下， 错误地定义多个全局变量的程序将通过链接器， 而不产生任何警告信息。 
由此得到的程序会产生令人迷惑的运行时行为，而且非常难以调试。  这里将向你展示这是如何发生的，以及该如何避免它。

理解链接器可以帮助你理解如何解析引用、什么是库以及链接器如何使用库解析引用的。

