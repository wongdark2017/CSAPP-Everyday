由于会使用地址运算符，调用代码必须分配一个栈帧。为局部变量和函数参数建立栈帧，将函数参数加载至寄存器。用leaq指令生成到这些位置的指针。程序结束，栈指针增加，释放栈帧。

3.7.5 寄存器中的局部存储空间
寄存器组是唯一被所有过程共享的资源。确保当一个过程调用另一个过程时，被调用者不会覆盖调用者稍后会使用的寄存器值。x86-64采用了一组统一的寄存器使用惯例。

被调用者保存寄存器：根据惯例，寄存器%rbx、%rbp和%r12~%r15被划分为被调用者保存寄存器。当P调用过程Q时，Q必须保存这些寄存器的值，保证Q返回到P时与Q被调用时的值是一致的。要么不改变，要么把原始值压入栈，改变寄存器的值，然后在返回前从栈中弹出旧值。

调用者保存寄存器：P在某寄存器中有局部数据，P调用Q，Q可以随意修改这个寄存器。
