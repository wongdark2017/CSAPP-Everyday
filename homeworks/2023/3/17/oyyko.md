链接器做了什么？

主要负责做两件事情

第一步：符号解析 Symbol resolution

我们在代码中会声明变量及函数，之后会调用变量及函数，所有的符号声明都会被保存在符号表(symbol table)中，而符号表会保存在由汇编器生成的 object 文件中（也就是 .o 文件）。符号表实际上是一个结构体数组，每一个元素包含名称、大小和符号的位置。

在 symbol resolution 阶段，链接器会给每个符号应用一个唯一的符号定义，用作寻找对应符号的标志。

第二步：重定位 Relocation

这一步所做的工作是把原先分开的代码和数据片段汇总成一个文件，会把原先在 .o 文件中的相对位置转换成在可执行程序的绝对位置，并且据此更新对应的引用符号（才能找到新的位置）