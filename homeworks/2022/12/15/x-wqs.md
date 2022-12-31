访问主存

数据流通过称为总线bus的共享电子电路在处理器和DRAM主存之间来来回回，每次CPU和主存之间的数据传送都是通过一系列步骤来完成的，这些步骤称为总线事务。读事务从主存传送数据到CPU，写事务从CPU传送数据到主存。总线是一组并行的导线，能携带地址、数据和控制信号。 

磁盘存储

读信息为毫秒级，比DRAM读慢了10万倍，比从SRAM读慢了100万倍。磁盘由盘片构成，每个盘片有两面或称为表面，表现覆盖着磁性记录材料，5400~15000转每分钟。每个表面有一组称为磁道的同心圆组成。每个磁道分为一组扇区，每个扇区包含相等数量的数据位。扇区之间由间隙分隔开，间隙中不存储数据位，用来存储标识扇区的格式化为。

磁盘容量：可记录最大位数为最大容量。记录密度、磁道密度、面密度。