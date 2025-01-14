## P384-388
存储单元包含一个存储缓冲区，它包含已经被发射到存储单元而又还没有完成的存储操作的地址和数据。提供这样一个缓冲区，使得一系列存储操作补不必等待每个操作都更新高速缓存就能执行。当一个加载操作发生时，它必须检查缓冲区中的条目，看有没有地址匹配。若有地址匹配，就取出相应的数据条目作为加载操作的结果。

对于寄存器操作，在指令被译码成操作操作的时候，处理器就可以确定哪些指令会影响其他哪些指令。另一方面，对于内存操作，只有计算出加载和存储的地址，处理器才能确定哪些指令会影响其他的哪些。

优化性能基本策略：高级设计（选择适当的算法和数据结构），基本编码原则（消除连续的函数调用，消除不必要的内存引用），低级优化。
