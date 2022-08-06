# Ch8 Exceptional Control Flow

## 8.5 Signals

### 8.5.3 Receiving Signals

当内核把进程从内核模式切换到用户模式下时，会检查该进程的未被阻塞的待处理信号的集合：

* 如果这个集合为空，则内核将控制传递给当前进程的逻辑控制流中的下一条指令。
* 如果集合非空，那么内核选择集合中的某个信号 k，并且强制进程接受信号 k 并进行特定行为，完毕后将将控制传递给当前进程的逻辑控制流中的下一条指令。

每个信号的默认行为是下面中的一种：

* 进程终止
* 进程终止并转储内存
* 进程停止或挂起，直至被 SIGCONT 信号重启
* 进程忽略该信号

可以通过 signal 函数修改信号的默认行为，但 SIGSTOP 和 SIGKILL 的默认信号不能修改。