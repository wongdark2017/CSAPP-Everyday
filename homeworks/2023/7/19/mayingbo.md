### 7.19

1. 在内存层次结构中，缓存（发音为“cash”）通常是一个小型、快速的存储设备，它充当了存储在更大、速度较慢的设备中的数据对象的临时存储区域

2. 内存层次结构的核心思想是对于每个级别k，速度更快、规模更小的存储设备充当了更大、速度较慢的存储设备的缓存。

   #### 块存储

   * 级别k + 1上的存储被划分为称为块的连续数据对象块。每个块都有一个唯一的地址或名称，用于区分它与其他块。块可以是固定大小（通常情况）或可变大小（例如，存储在Web服务器上的远程HTML文件）。

   * 数据始终以块大小的传输单元在级别k和级别k + 1之间进行复制。重要的是要意识到，在层次结构中，块大小在任何相邻级别之间是固定的，但其他级别之间的块大小可能不同

   * 一般来说，层次结构中较低（离CPU更远）的设备具有更长的访问时间，因此倾向于使用更大的块大小以分摊这些较长的访问时间。

     通常这也就是快存储的概念入门！！
     
   * 缓存未命中是指如果数据对象d在k级别未缓存，则会导致缓存未命中。在发生未命中时，k级别的缓存会从k + 1级别的缓存中获取包含d的块，如果k级别的缓存已经满了，则可能会覆盖一个现有的块。->LRU覆盖
   
   * 在k级别的缓存从k + 1级别获取块之后，程序可以像之前一样从k级别读取d。如果从k级别的缓存中读取块12，则会导致缓存未命中，因为块12当前未缓存在k级别。一旦它从k + 1级别复制到k级别，块12将在期望后续访问中保留在那里。
   
     缓存未命中有不同类型。当k级别的缓存为空时，任何数据对象的访问都会未命中。一个空的缓存有时被称为冷缓存，这种类型的未命中称为强制性未命中或冷未命中。冷未命中很重要，因为它们通常是暂时性的事件，在缓存被重复访问后可能不会在稳态下发生。
   
     每当发生未命中时，k级别的缓存必须实现一些放置策略，以确定从k + 1级别获取的块应该放在哪个位置。最灵活的放置策略是允许从k + 1级别的任何块存储到k级别的任何块。对于位于内存层次结构高端（接近CPU）且以硬件实现且速度至关重要的缓存来说，这种策略通常太昂贵，因为随机放置的块定位开销大。