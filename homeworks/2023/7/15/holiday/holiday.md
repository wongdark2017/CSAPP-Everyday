读取数据的方式：

盘片逆时针旋转，读写头会检测bit，发送到控制器，传回CPU

读取数据的时间取决于下面3个因素：

1. 移动磁头被称为**寻道时间**
2. 磁盘旋转到读写头的下方被称为，被称为**旋转延迟**
3. **传送时间**：该轨道在读写头下通过的时间

3个因素决定了时间的平均值

磁盘连接到CPU和内存

![image-20230716110706819](image/image-20230716110706819.png)