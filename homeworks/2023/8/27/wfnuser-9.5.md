- # 9.5 VM as a Tool for Memory Protection  
	- VM 另一个作用是起到内存保护的功能  
	- 用户态的进程不应该修改只读的代码区，也不应该读写任何内核的代码或者数据结构；也不该读到其他进程的司有内存；也不能在其他进程不感知的前提下修改被共享的虚拟页  
	- 这是一种天然的扩展方式；SUP表示该页只能被内核态的进程访问；READWRITE表示读写权限。  
	- 如果指令违反了相关权限，CPU会出发一个 general protection fault 并陷入异常 SIGSEGV  