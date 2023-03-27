考虑一个C程序，有两个文件p1.c和p2.c。我们用Unix命令行编译这些代码：

Linux> gcc -Og -o p p1.c p2.c
实际上gcc命令调用了一整套的程序，将源代码转化成可执行代码：

C预处理器扩展源代码，插入所有用#include命定指定的文件，扩展所有用#define声明指定的宏。
编译器产生两个源文件的汇编代码，名字分别为p1.s和p2.s。
汇编器将汇编代码转化成二进制目标代码文件p1.o和p2.o。
链接器将两个目标代码文件与实现库函数（例printf）的代码合并，并产生最终的可执行代码文件p。

由指令集体系结构或指令集架构来定义机器级程序的格式和行为，它定义了处理器状态、指令的格式、以及每条指令对状态的影响。
机器级程序使用的内存地址是虚拟地址，提供的内存模型看上去是一个很大的、按字节寻址的数组。