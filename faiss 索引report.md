## OndiskInvertedList

通过内存映射（memory map）技术，将倒排列表储存在磁盘当中。

整个倒排文件被存储为一个个mmap内存块。每个单独的倒排列表是这个大内存块的一个分段。

像倒排列表中添加数据很慢

### **最佳实践**

**增量添加**

在内存中维护一个 ArrayInvertedList，然后通过 merge_from 一次性将其放大磁盘上的 OndiskInvertedList 中。

**查询预取**

prefetch_lists()方法：查询时先查清查询向量属于哪些倒排列表，prefetch_lists() 接受这些列表 ID，从而可以将这些列表并行地从磁盘预加载到操作系统的缓存中
