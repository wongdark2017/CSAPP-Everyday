# CSAPP_12_10

**提示：处理器的设计步骤**

1. 1.分析指令，推导出数据通路需求
2. 2.为所需的数据通路选择合适的组件
3. 3.连接各个组件建立数据通路
4. 4.分析指令的实现，以确定控制信号
5. 5.集成控制信号，形成完整的控制逻辑

**单周期处理器设计**：数据通路 + 实现控制逻辑  (本质 = 组合逻辑电路 + 时序逻辑电路)

**流水线技术：**现代处理器借鉴了汽车生产的流水线技术，使得指令能够并行执行（ILP）

流水线并不会缩短单条指令的执行时间（甚至会增加时间）， 但是提高了指令的吞吐率。流水线深度也不是越深越好，一方面由于流水线寄存器本身会带来额外的开销，另外一方面流水线越深，由分支预测失败带来的性能损失会更大，因此实际需要考虑折中。

**结构冒险**：所需的硬件资源正在被之前的指令工作，解决方案：等待Stall，或者增加硬件资源，比如增加寄存器的端口数量，或者指令和数据Cache分开存储.

**数据冒险**：需要等待之前的指令完成写操作，解决方案：等待Stall，或者提前转发Forwarding，但是无法解决所有的数据依赖问题（例如需要访存的情况）

**控制冒险**： 需要根据之前指令的结果决定下一步的行为，解决方案：等待Stall，分支预测（硬件实现的动态预测，比如branch target buffer，branch history table等机制），编译器实现的分支合并等。
