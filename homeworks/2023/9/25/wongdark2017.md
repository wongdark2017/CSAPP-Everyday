# CSAPP读书笔记


最后的四个标识位（CF, ZF, SF, OF）就是用来辅助程序的流程控制的，意思是：

* CF: Carry Flag (针对无符号数)
* ZF: Zero Flag
* SF: Sign Flag (针对有符号数)
* OF: Overflow Flag (针对有符号数)

可以看到以上这四个标识位，表示四种不同的状态，举个例子，假如我们有一条诸如 `t = a + b` 的语句，汇编之后假设用的是 `addq Src, Dest`，那么根据这个操作结果的不同，会相应设置上面提到的四个标识位，而因为这个是执行类似操作时顺带尽心设置的，称为隐式设置，例如：

* 如果两个数相加，在最高位还需要进位（也就是溢出了），那么 CF 标识位就会被设置
* 如果 t 等于 0，那么 ZF 标识位会被设置
* 如果 t 小于 0，那么 SF 标识位会被设置
* 如果 2’s complement 溢出，那么 OF 标识位会被设置为 1（溢出的情况是 `(a>0 && b > 0 && t <0) || (a<0 && b<0 && t>=0)`）