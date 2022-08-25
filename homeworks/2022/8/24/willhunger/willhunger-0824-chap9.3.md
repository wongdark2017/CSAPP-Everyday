# Ch9 VM as a Tool for Caching

## 9.3 Address Spaces

虚拟内存被组织为一个由存放在磁盘上的 N 个连续的字节大小的单元组成的数组、

VM 系统将虚拟内存分割为大小固定的块（虚拟页）来处理这个问题，同样，物理内存被分割为物理页( Page frame，页帧)。

在任意时刻，虚拟页面的集合都分为三个不相交的子集：

* 未分配的：VM 系统还未分配或创建的页，不占用任何磁盘空间。
* 缓存的：当前已缓存在物理内存中的已分配页。
* 未缓存的：未缓存在物理内存中的已分配页。
