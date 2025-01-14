- ## 8.4.3 Reaping Child Processes  
	- 进程终止后并不会马上被内核移除，直到被父进程 reap 为止，该进程都会存在  
	- reap子进程时，kernel将子进程的退出状态传给父进程，然后 discard 被结束的进程  
	- 一个没有被reap的终止进程被称为僵尸进程  
	- init 进程的进程号为1 在系统启动时被创建 且永远不会被终止  
	- 调用 waitpid 来等待子进程结束  
	- waitpid 默认会阻塞直到 wait set 的进程结束为止； 如果进行该系统调用时 wait set 已经结束， waitpid 立刻返回； 返回值为 PID； 返回时，子进程已经被 reap 并且内核会移除所有该进程相关的 trace  
	- 参数 pid 如果大于0，则表示要等待的子进程ID； 如果 = -1 则表示所有当前进程的子进程及其本身都是 wait set  
	- options 有三种取值用于控制等待行为  
		- WNOHANG 如果没有子进程在wait set中则立刻返回  
		- WUNTRACED 阻塞直到 wait set 中的进程终止  
		- WCONTINUED 阻塞直到 wait set 中的进程终止或者暂停的进程恢复  
	- 不同的退出状态  
		- WIFEXITED  
		- WEXITSTATUS  
		- WIFSIGNALED  
		- WTERMSIG  
		- WIFSTOPPED  
		- WSTOPSIG  
		- WIFCONTINUED  
	- Error Conditions  
		- 如果当前进程没有子进程 waitpid return -1 并设置 errno 为 ECHILD  
		- 如果 waitpid 被信号打断， return -1 并返回 EINTR  
	-  