第一个进程写入后， 文件（i节点）的偏移已经改变， 第二个进程再写会覆盖第一个进程刚写的内容。 而是用O_APPEND的open,会使内核每次对文件写之前，都将进程的当前偏移量（file对象中的）设置到
文件的尾端处（i节点的当前文件长度）。

2个独立进程打开同一文件， 对应不同的file对象， 每个进程调用close只影响本进程“打开文件计数”。
