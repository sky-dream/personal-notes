# Data structure

## 定义

在[计算机科学](https://zh.wikipedia.org/wiki/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6)中，**数据结构**（英语：data structure）是计算机中存储、组织[数据](https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE)的方式。

数据结构意味着[接口](https://zh.wikipedia.org/wiki/%E4%BB%8B%E9%9D%A2_%28%E9%9B%BB%E8%85%A6%E7%A7%91%E5%AD%B8%29)或[封装](https://zh.wikipedia.org/wiki/%E5%B0%81%E8%A3%85_%28%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6%29)：一个数据结构可被视为两个函数之间的接口，或者是由[数据类型](https://zh.wikipedia.org/wiki/%E6%95%B8%E6%93%9A%E9%A1%9E%E5%9E%8B)联合组成的存储内容的访问方法封装。

大多数数据结构都由[数列](https://zh.wikipedia.org/wiki/%E6%95%B0%E5%88%97)、[记录](https://zh.wikipedia.org/wiki/%E8%AE%B0%E5%BD%95)、[可辨识联合](https://zh.wikipedia.org/wiki/%E6%A0%87%E7%AD%BE%E8%81%94%E5%90%88)、[引用](https://zh.wikipedia.org/wiki/%E5%8F%83%E7%85%A7)等基本类型构成。举例而言，可为空的引用（nullable reference）是引用与可辨识联合的结合体，而最简单的链式结构[链表](https://zh.wikipedia.org/wiki/%E9%93%BE%E8%A1%A8)则是由记录与可空引用构成。

数据结构可透过[编程语言](https://zh.wikipedia.org/wiki/%E7%BC%96%E7%A8%8B%E8%AF%AD%E8%A8%80)所提供的[数据类型](https://zh.wikipedia.org/wiki/%E6%95%B8%E6%93%9A%E9%A1%9E%E5%9E%8B)、[引用](https://zh.wikipedia.org/wiki/%E5%8F%83%E7%85%A7)及其他操作加以实现。一个设计良好的数据结构，应该在尽可能使用较少的时间与空间资源的前提下，支持各种程序运行。

不同种类的数据结构适合不同种类的应用，部分数据结构甚至是为了解决特定问题而设计出来的。例如[B树](https://zh.wikipedia.org/wiki/B%E6%A0%91)即为加快树状结构访问速度而设计的数据结构，常被应用在数据库和文件系统上。

正确的数据结构选择可以提高[算法](https://zh.wikipedia.org/wiki/%E6%BC%94%E7%AE%97%E6%B3%95)的效率（请参考[算法效率](https://zh.wikipedia.org/w/index.php?title=%E6%BC%94%E7%AE%97%E6%B3%95%E6%95%88%E7%8E%87&action=edit&redlink=1)）。在[计算机程序](https://zh.wikipedia.org/wiki/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A8%8B%E5%BA%8F)设计的过程中，选择适当的数据结构是一项重要工作。许多大型系统的编写经验显示，[程序设计](https://zh.wikipedia.org/wiki/%E7%A8%8B%E5%BC%8F%E8%A8%AD%E8%A8%88)的困难程度与最终成果的质量与表现，取决于是否选择了最适合的数据结构。

[系统架构](https://zh.wikipedia.org/wiki/%E7%B3%BB%E7%BB%9F%E6%9E%B6%E6%9E%84)的关键因素是数据结构而非算法的见解，导致了多种形式化的设计方法与[编程语言](https://zh.wikipedia.org/wiki/%E7%BC%96%E7%A8%8B%E8%AF%AD%E8%A8%80)的出现。绝大多数的语言都带有某种程度上的[模块化](https://zh.wikipedia.org/wiki/%E6%A8%A1%E5%9D%97_%28%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%29)思想，透过将数据结构的具体实现封装隐藏于用户界面之后的方法，来让不同的应用程序能够安全地重用这些数据结构。[C++](https://zh.wikipedia.org/wiki/C%2B%2B)、[Java](https://zh.wikipedia.org/wiki/Java)、[Python](https://zh.wikipedia.org/wiki/Python)等[面向对象](https://zh.wikipedia.org/wiki/%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E7%9A%84%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1)的编程语言可使用[类 \(计算机科学\)](https://zh.wikipedia.org/wiki/%E7%B1%BB_%28%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6%29)来达到这个目的。

因为数据结构概念的普及，现代编程语言及其[API](https://zh.wikipedia.org/wiki/%E8%BF%90%E8%A1%8C%E7%8E%AF%E5%A2%83)中都包含了多种默认的数据结构，例如 C++ [标准模板库](https://zh.wikipedia.org/wiki/%E6%A0%87%E5%87%86%E6%A8%A1%E6%9D%BF%E5%BA%93)中的容器、[Java集合框架](https://zh.wikipedia.org/wiki/Java%E9%9B%86%E5%90%88%E6%A1%86%E6%9E%B6)以及微软的[.NET Framework](https://zh.wikipedia.org/wiki/.NET_Framework)。

### 常见的数据结构

* [堆栈](https://zh.wikipedia.org/wiki/%E5%A0%86%E7%96%8A)（Stack）
* [队列](https://zh.wikipedia.org/wiki/%E9%98%9F%E5%88%97)（Queue）
* [数组](https://zh.wikipedia.org/wiki/%E9%99%A3%E5%88%97)（Array）
* [链表](https://zh.wikipedia.org/wiki/%E9%93%BE%E8%A1%A8)（Linked List）
* [树](https://zh.wikipedia.org/wiki/%E6%A0%91_%28%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%29)（Tree）
* [堆积](https://zh.wikipedia.org/wiki/%E5%A0%86_%28%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%29)（Heap）
* [散列表](https://zh.wikipedia.org/wiki/%E6%95%A3%E5%88%97%E8%A1%A8)（Hash table）

## 高级数据结构

* 优先队列 
* 图 
* 前缀树 
* 线段树 
* 树状数组



