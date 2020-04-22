# 优先队列

 **优先队列**是[计算机科学](https://zh.wikipedia.org/wiki/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6)中的一类[抽象数据类型](https://zh.wikipedia.org/wiki/%E6%8A%BD%E8%B1%A1%E6%95%B8%E6%93%9A%E9%A1%9E%E5%9E%8B)。优先队列中的每个元素都有各自的优先级，优先级最高的元素最先得到服务；优先级相同的元素按照其在优先队列中的顺序得到服务。优先队列往往用[**堆**](https://zh.wikipedia.org/wiki/%E5%A0%86_%28%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%29)来实现。

### 操作

优先队列至少需要支持下述操作：

* 插入带优先级的元素（insert\_with\_priority）
* 取出具有最高优先级的元素（pull\_highest\_priority\_element）
* 查看最高优先级的元素（peek）：O\(1\) 时间复杂度

其它可选的操作：

* 检查优先级高的一批元素
* 清空优先队列
* 批插入一批元素
* 合并多个优先队列
* 调整一个元素的优先级

#### 典型实现

出于性能考虑，优先队列用[堆](https://zh.wikipedia.org/wiki/%E5%A0%86_%28%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%29)来实现，具有O\(log n\)时间复杂度的插入元素性能，O\(n\)的初始化构造的时间复杂度。如果使用[自平衡二叉查找树](https://zh.wikipedia.org/wiki/%E5%B9%B3%E8%A1%A1%E6%A0%91)，插入与删除的时间复杂度为O\(log n\)，构造二叉树的时间复杂度为O\(n log n\)。

从计算复杂度的角度，优先级队列等价于[排序算法](https://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95)。

有一些特殊的[堆](https://zh.wikipedia.org/wiki/%E5%A0%86_%28%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%29)为优先队列的实现提供了额外的性能：[二叉堆](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%8F%89%E5%A0%86)的插入与提取操作的时间复杂度为O\(log n\)，并可以常量时间复杂度的peek操作。[二项堆](https://zh.wikipedia.org/wiki/%E4%BA%8C%E9%A1%B9%E5%A0%86)提供了几种额外操作。[斐波那契堆](https://zh.wikipedia.org/wiki/%E6%96%90%E6%B3%A2%E9%82%A3%E5%A5%91%E5%A0%86)的插入、提取、修改元素优先级等操作具有[分摊](https://zh.wikipedia.org/wiki/%E5%B9%B3%E6%91%8A%E5%88%86%E6%9E%90)常量时间复杂度，[\[1\]](https://zh.wikipedia.org/wiki/%E5%84%AA%E5%85%88%E4%BD%87%E5%88%97#cite_note-CLRS-1)，但删除操作的时间复杂度为O\(log n\)。[Brodal queue](https://zh.wikipedia.org/w/index.php?title=Brodal_queue&action=edit&redlink=1)具有最糟糕情况下的常量复杂度但算法相当复杂因而不具有实用性。

对于整型、浮点型等具有有限值域的元素的数据类型，优先队列有更快的实现。

### 库实现

优先队列是计算机科学中的一类"[容器数据类型](https://zh.wikipedia.org/wiki/%E9%9B%86%E5%90%88_%28%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6%29)"。

[标准模板库](https://zh.wikipedia.org/wiki/%E6%A0%87%E5%87%86%E6%A8%A1%E6%9D%BF%E5%BA%93)（STL）以及1998年的[C++](https://zh.wikipedia.org/wiki/C%2B%2B)标准确定优先队列是标准模板库的[容器](https://zh.wikipedia.org/wiki/%E5%AE%B9%E5%99%A8_%28%E6%8A%BD%E8%B1%A1%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%29)适配器[模板](https://zh.wikipedia.org/wiki/%E6%A8%A1%E6%9D%BF_%28C%2B%2B%29)。其实现了一个需要三个参数的最大优先队列：比较函数（缺省情况是小于函数less&lt;T&gt;）、存储数据所用的容器类型（缺省情况是向量vector&lt;T&gt;）以及指向序列开始和结束位置的两个[迭代器](https://zh.wikipedia.org/wiki/%E8%BF%AD%E4%BB%A3%E5%99%A8)。和标准模板库中其他的真实容器不同，优先队列不允许使用其元素类型的迭代器，而必须使用优先队列抽象数据类型的迭代器。标准模板库还实现了支持随机访问数据容器的优先队列--二叉最大[堆](https://zh.wikipedia.org/wiki/%E5%A0%86_%28%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%29)。[Boost C++库](https://zh.wikipedia.org/wiki/Boost_C%2B%2B_Libraries)也在其中实现了堆结构。

[Python](https://zh.wikipedia.org/wiki/Python)的[heapq](https://docs.python.org/library/heapq.html)模块实现了在链表基础上的二叉最小堆。

[Java](https://zh.wikipedia.org/wiki/Java)库中的[`PriorityQueue`](http://download.oracle.com/javase/7/docs/api/java/util/PriorityQueue.html)类实现了最小优先队列。

[Go](https://zh.wikipedia.org/wiki/Go)库中的[container/heap](https://golang.org/pkg/container/heap/)模块实现了一个可以在任何兼容数据结构上构建的最小堆。

[PHP标准库](https://zh.wikipedia.org/wiki/PHP%E6%A0%87%E5%87%86%E5%BA%93)包括了一个优先队列[SplPriorityQueue](http://us2.php.net/manual/en/class.splpriorityqueue.php)。

[苹果](https://zh.wikipedia.org/wiki/%E8%8B%B9%E6%9E%9C%E5%85%AC%E5%8F%B8)的[Core Foundation](https://zh.wikipedia.org/w/index.php?title=Core_Foundation&action=edit&redlink=1)框架包括了一个最小堆结构[CFBinaryHeap](http://developer.apple.com/library/mac/#documentation/CoreFoundation/Reference/CFBinaryHeapRef/Reference/reference.html)。

### 应用

 优先队列常用于操作系统的[任务调度](https://zh.wikipedia.org/wiki/%E8%B0%83%E5%BA%A6_%28%E8%AE%A1%E7%AE%97%E6%9C%BA%29)，也是[贪心算法](https://zh.wikipedia.org/wiki/%E8%B4%AA%E5%BF%83%E7%AE%97%E6%B3%95)的重要组成部分。

示例： leetcode 253. meeting rooms

