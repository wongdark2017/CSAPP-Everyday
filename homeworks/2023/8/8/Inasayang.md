#### 处理器读并解释存在内存中的指令

##### 系统的硬件组成

![](https://inasa.dev/image/csapp/1.png)



-   总线
    -   贯穿整个系统的一组电子管道，称为***总线***
    -   负责携带信息字节，在各个部件传递
    -   通常传送定长的字节块，就是字（`word`），32位为4字节，64位位8字节
-   IO设备
    -   键盘，鼠标，显示器，磁盘
    -   每个IO设备通过一个控制器或适配器与IO总线相连
    -   控制器和适配器的区别主要在于各自的封装方式
        -   控制器是IO设备本身或系统的主板上的芯片组
        -   适配器是一块插在主板插槽上的卡
-   主存
    -   临时存储设别
    -   物理上，主存是由一组***动态随机存取存储器***（`DRAM`）芯片组成
    -   逻辑上，存储器是一个线性的字节数组，每个字节都有唯一的地址，地址从0开始
-   处理器
    -   中央处理单元（`CPU`），简称处理器
    -   解释或执行存在主存中指令的引擎
    -   处理器的核心是一个大小为一个字的存储设备（或寄存器），称为***程序计数器***（`PC`）
    -   在任何时刻，`PC`都指向主存中的某条机器语言指令（含有该条指令的地址）
    -   从系统通电开始知道断电，处理器一直不断执行`PC`指向的指令，再更新`PC`，使其指向下一条指令
    -   处理器是按照一个非常简单的指令执行模型来操作，模型由***指令集架构***决定
        -   指令按照严格的顺序执行，执行一条指令包含一系列步骤
        -   处理器从`PC`指向的内存处读取指令
        -   解释指令中的位
        -   执行指令指示的简单操作
        -   更新`PC`，使其指向下一条指令（这条指令不一定和在内存中刚刚执行的指令相邻）
    -   简单操作围绕主存，寄存器文件（`register file`）和算数/逻辑单元（`ALU`）进行
        -   寄存器文件是一个小的存储设备，由一些单个字长的寄存器组成，每个寄存器都有唯一的名字
        -   `ALU`计算新的数据和地址值
        -   简单操作例子
            -   加载
                -   从主存复制一个字节或一个字到寄存器，来覆盖寄存器原来的内容
            -   存储
                -   从寄存器复制一个字节或一个字到主存上的某个位置，来覆盖原来的内容
            -   操作
                -   把两个寄存器的内容复制到`ALU`, `ALU`进行算数运算，再把结果放到一个寄存器中，来覆盖原来的内容
            -   跳转
                -   从指令本身中抽取一个字，复制到`PC`中，来覆盖原来的内容
    -   现代处理器使用非常复杂的机制来加速程序的执行
    -   处理器的***指令集架构***和处理器的***微体系结构***
        -   ***指令集架构***描述每条机器代码指令的效果
        -   ***微体系结构***描述的是处理器实际上是如何实现的

##### 运行hello程序

![](https://inasa.dev/image/csapp/2.png)

-   在输入`./hello`后，`shell`程序将字符逐一读入寄存器，再放入内存中
-   敲回车键时，`shell`程序知道了命令的结束
-   `shell`执行一系列指令来加载可执行的`hello`文件
-   这些指令将`hello`目标文件中的代码和数据从磁盘复制到主存中
-   使用***直接存储器存取***（`DMA`），数据可以不通过处理器，直接从磁盘到主存

![](https://inasa.dev/image/csapp/3.png)

-   一旦`hello`中的代码和数据被加载到主存中，处理器就开始执行`main`中的机器语言指令
-   指令将`“hello, world\n”`字符串中的字节从主存复制到寄存器文件
-   再从寄存器文件复制到显示设备，最终显示再屏幕上



#### 高速缓存至关重要

-   可以看到，好多地方都是复制，复制就是开销
-   机械原理
    -   较大的存储设备要比较小的存储设备运行慢
    -   快速设备的造价要高于同类的低速设备
-   针对处理器和主存的差异，系统设计者采用了更小更快的存储设备，***高速缓存储存器***（`cache memory`），简称cache或高速缓存，作为暂时的集结区域，存放处理器近期可能会需要的信息

![](https://inasa.dev/image/csapp/4.png)

-   L1和L2高速缓存使用一种叫做***静态随机访问存储器***（`SRAM`）的硬件技术



#### 存储设备形成层次结构

![](https://inasa.dev/image/csapp/5.png)

#### 操作系统管理硬件

![](https://inasa.dev/image/csapp/6.png)





-   操作系统是程序和硬件之间插入的一层软件，程序依靠操作系统提供的服务
-   所有应用程序对硬件的操作都必须通过操作系统
-   操作系统的两个基本功能
    -   防止硬件被失控的应用程序滥用
    -   向应用程序提供简单一致的机制来控制复杂又各不相同的低级硬件设备
-   操作系统通过三个基本的抽象概念来实现两个基本功能
    -   进程
        -   对处理器，主存和IO设备的抽象表示
    -   虚拟内存
        -   对主存和磁盘IO设备的抽象表示
    -   文件
        -   对IO设备的抽象表示

##### 进程

-   是操作系统对一个正在运行的程序的一种抽象
-   并发运行，一个进程的指令和另一个进程的指令是交错执行的
-   操作系统执行交错执行的机制称为***上下文切换***
-   上下文，一种状态，操作系统保持跟踪进程运行所需的所有状态信息
    -   包括`PC`，寄存器文件的当前值，主存的内容

![](https://inasa.dev/image/csapp/7.png)

-   从一个进程到另一个进程的转换是由操作系统内核（`kernel`）管理的
-   内核是操作系统代码常驻主存的部分
-   当应用程序需要操作系统的某些操作时，执行一条***系统调用***（`system call`）指令，将控制权传递给内核
-   内核执行被请求的操作并返回给应用程序
-   内核不是一个独立的进程，是系统管理全部进程所有代码和数据结构的集合



##### 线程

-   一个进程由多个称为线程的执行单元组成
-   每个线程都运行在进程的上下文中，共享同样的代码和全局数据



##### 虚拟内存

-   为每个进程提供了一个假象
    -   每个进程都在独占的使用主存
    -   每个进程看到的内存都是一致的，称为***虚拟地址空间***

![](https://inasa.dev/image/csapp/8.png)

-   地址空间最上面的区域是保留给操作系统中的代码和数据的，对所有的进程都是一样
-   地址空间最下面的区域是存放用户进程定义的代码和数据
-   每个进程看到的虚拟地址空间由大量准确定义的区构成，每个区都有专门的功能，从下往上依次是
    -   程序代码和数据
        -   所有进程的代码都是从同一固定地址开始
        -   紧接是和C全局变量相对应的数据位置
        -   代码和数据区是直接按照可执行目标文件的内容初始化的
    -   堆
        -   代码和数据区后紧接着运行时堆
        -   代码和数据区在进程一开始运行时就被指定了大小
        -   堆可以在运行时动态扩缩
    -   共享库
        -   地址空间的中间部分区域用来存放C标准库和数学库这种共享库的代码和数据区域
    -   栈
        -   用户栈
        -   编译器用来实现函数调用
        -   在执行期间动态扩缩
        -   调用函数，栈增长
        -   函数返回，栈收缩
    -   内核虚拟内存
        -   为内核保留
        -   不允许应用程序读写或直接调用内核代码定义的函数
        -   必须调用内核来执行操作



##### 文件

-   字节序列



#### 系统之间利用网络通信

![](https://inasa.dev/image/csapp/9.png)

-   系统从主存复制一串字节到网络适配器，数据流经过网络发送到另一台机器



#### 重要主题

##### Amdahl定律

-   对系统的某个部分加速时，其对系统整体性能的影响取决于该部分的重要性和加速程度

![](https://inasa.dev/image/csapp/10.png)



##### 并发与并行

###### 线程级并发

![](https://inasa.dev/image/csapp/11.png)

如上一个多核处理器的组织架构，4个处理器核集成在一个芯片上

微处理器有4个CPU核，每个都有自己的L1和L2高速缓存

L1高速缓存分为两个部分

-   一个保存最近取到的指令
-   另一个存放数据



超线程（同时超线程，simultaneous multi-threading）

-   允许一个CPU执行多个控制流
-   CPU的某些硬件有多个备份，如PC和寄存器文件，但是其他硬件只有一份，如执行浮点算术运算的单元



###### 指令集并发

-   同时执行多条指令
-   超标量（super-scalar）处理器，比一个周期一条指令更快的执行速率



###### 单指令，多数据并行

-   允许一条指令产生多个可以并行执行的操作，SIMD并行
-   提高了处理影像，声音和视频数据应用的执行速度
-   用编译器支持的特殊的向量数据类型来写程序
    -   GCC支持向量数据类型



##### 计算机系统抽象的重要性

![](https://inasa.dev/image/csapp/12.png)

-   虚拟机，对整个计算机的抽象，包括操作系统，处理器和程序



Pp.5-20