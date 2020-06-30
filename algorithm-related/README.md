# Algorithm related

wikipedia 对算法的解释如下：

**算法**（algorithm），在[数学](https://zh.wikipedia.org/wiki/%E6%95%B8%E5%AD%B8)（[算学](https://zh.wikipedia.org/wiki/%E7%AE%97%E5%AD%B8)）和[计算机科学](https://zh.wikipedia.org/wiki/%E9%9B%BB%E8%85%A6%E7%A7%91%E5%AD%B8)之中，为任何一系列良定义的具体计算步骤，常用于[计算](https://zh.wikipedia.org/wiki/%E8%A8%88%E7%AE%97)、[数据处理](https://zh.wikipedia.org/w/index.php?title=%E6%95%B8%E6%93%9A%E8%99%95%E7%90%86&action=edit&redlink=1)和[自动推理](https://zh.wikipedia.org/wiki/%E8%87%AA%E5%8A%A8%E6%8E%A8%E7%90%86)。作为一个[有效方法](https://zh.wikipedia.org/w/index.php?title=%E6%9C%89%E6%95%88%E6%96%B9%E6%B3%95&action=edit&redlink=1)，算法被用于计算[函数](https://zh.wikipedia.org/wiki/%E5%87%BD%E6%95%B8)，它包含了一系列定义清晰的指令[\[3\]](https://zh.wikipedia.org/wiki/%E7%AE%97%E6%B3%95#cite_note-3)，并可于[有限的](https://zh.wiktionary.org/wiki/Special:Search/%E6%9C%89%E9%99%90%E7%9A%84)时间及空间内清楚的表述出来。

算法中的指令描述的是一个[计算](https://zh.wikipedia.org/wiki/%E8%A8%88%E7%AE%97)，当其[运行](https://zh.wikipedia.org/w/index.php?title=%E5%9F%B7%E8%A1%8C&action=edit&redlink=1)时能从一个初始状态和初始输入（可能为[空](https://zh.wikipedia.org/wiki/%E7%A9%BA%E5%AD%97%E5%85%83%E4%B8%B2)）开始，经过一系列**有限**而清晰定义的状态最终产生**输出**并**停止**于一个终态。一个状态到另一个状态的转移不一定是[确定的](https://zh.wikipedia.org/wiki/%E7%A1%AE%E5%AE%9A%E6%80%A7%E7%AE%97%E6%B3%95)。包括[随机化算法](https://zh.wikipedia.org/wiki/%E9%9A%A8%E6%A9%9F%E5%8C%96%E7%AE%97%E6%B3%95)在内的一些算法，都包含了一些随机输入。

### 特征

以下是[高德纳](https://zh.wikipedia.org/wiki/%E9%AB%98%E5%BE%B7%E7%BA%B3)在他的著作《[计算机程序设计艺术](https://zh.wikipedia.org/wiki/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%E8%89%BA%E6%9C%AF)》里对算法的特征归纳：[![MerkleTree1.JPG](https://upload.wikimedia.org/wikipedia/commons/thumb/1/12/MerkleTree1.JPG/200px-MerkleTree1.JPG)](https://zh.wikipedia.org/wiki/File:MerkleTree1.JPG)

1. 输入：一个算法必须有零个或以上输入量。
2. 输出：一个算法应有一个或以上输出量，输出量是算法计算的结果。
3. 明确性：算法的描述必须无歧义，以保证算法的实际执行结果是精确地符合要求或期望，通常要求实际运行结果是确定的。
4. 有限性：依据图灵的定义，一个算法是能够被任何[图灵完全](https://zh.wikipedia.org/wiki/%E5%9B%BE%E7%81%B5%E5%AE%8C%E5%85%A8)系统模拟的一串运算，而[图灵机](https://zh.wikipedia.org/wiki/%E5%9C%96%E9%9D%88%E6%A9%9F)只有有限个状态、有限个输入符号和有限个转移函数（指令）。而一些定义更规定算法必须在有限个步骤内完成任务。
5. 有效性：又称可行性。能够实现，算法中描述的操作都是可以通过已经实现的基本运算执行有限次来实现。

#### 常用设计模式

完全[遍历法](https://zh.wikipedia.org/w/index.php?title=%E9%81%8D%E6%AD%B7%E6%B3%95&action=edit&redlink=1)和不完全遍历法：在问题的解是有限离散解空间，且可以验证正确性和最优性时，最简单的算法就是把解空间的所有元素完全遍历一遍，逐个检测元素是否是我们要的解。这是最直接的算法，实现往往最简单。但是当解空间特别庞大时，这种算法很可能导致工程上无法承受的计算量。这时候可以利用不完全遍历方法——例如各种搜索法和规划法——来减少计算量。

[分治法](https://zh.wikipedia.org/wiki/%E5%88%86%E6%B2%BB%E6%B3%95)：把一个问题分割成互相独立的多个部分分别求解的思路。这种求解思路带来的好处之一是便于进行并行计算。

[动态规划](https://zh.wikipedia.org/wiki/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)法：当问题的整体最优解就是由局部最优解组成的时候，经常采用的一种方法。

[贪心算法](https://zh.wikipedia.org/wiki/%E8%B4%AA%E5%BF%83%E6%B3%95)：常见的近似求解思路。当问题的整体最优解不是（或无法证明是）由局部最优解组成，且对解的最优性没有要求的时候，可以采用的一种方法。

[线性规划](https://zh.wikipedia.org/wiki/%E7%BA%BF%E6%80%A7%E8%A7%84%E5%88%92)法：见条目。

简并法：把一个问题通过逻辑或数学推理，简化成与之等价或者近似的、相对简单的模型，进而求解的方法。

#### 常用实现方法

[递归方法](https://zh.wikipedia.org/wiki/%E9%80%92%E5%BD%92)与[迭代方法](https://zh.wikipedia.org/wiki/%E8%BF%AD%E4%BB%A3)

顺序计算、[并行计算](https://zh.wikipedia.org/wiki/%E5%B9%B6%E8%A1%8C%E8%AE%A1%E7%AE%97)和[分布式计算](https://zh.wikipedia.org/wiki/%E5%88%86%E5%B8%83%E5%BC%8F%E8%AE%A1%E7%AE%97)：顺序计算就是把形式化算法用编程语言进行单线程序列化后执行。

确定性算法和非确定性算法

精确求解和近似求解

### 分类

* 基本算法
  * [枚举](https://zh.wikipedia.org/wiki/%E6%9E%9A%E4%B8%BE)
  * [搜索](https://zh.wikipedia.org/wiki/%E6%90%9C%E7%B4%A2_%28%E8%AE%A1%E7%AE%97%E6%9C%BA%29)
    * [深度优先搜索](https://zh.wikipedia.org/wiki/%E6%B7%B1%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C%E7%B4%A2)
    * [广度优先搜索](https://zh.wikipedia.org/wiki/%E5%B9%BF%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C%E7%B4%A2)
    * [启发式搜索](https://zh.wikipedia.org/wiki/%E5%90%AF%E5%8F%91%E5%BC%8F%E6%90%9C%E7%B4%A2)
    * [遗传算法](https://zh.wikipedia.org/wiki/%E9%81%97%E4%BC%A0%E7%AE%97%E6%B3%95)
* [数据结构](https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84)的算法
* [数论与代数算法](https://zh.wikipedia.org/w/index.php?title=%E6%95%B0%E8%AE%BA%E4%B8%8E%E4%BB%A3%E6%95%B0%E7%AE%97%E6%B3%95&action=edit&redlink=1)
* [计算几何](https://zh.wikipedia.org/wiki/%E8%AE%A1%E7%AE%97%E5%87%A0%E4%BD%95)的算法
  * [凸包](https://zh.wikipedia.org/wiki/%E5%87%B8%E5%8C%85)算法
* [图论](https://zh.wikipedia.org/wiki/%E5%9B%BE%E8%AE%BA)的算法
  * [哈夫曼编码](https://zh.wikipedia.org/wiki/%E5%93%88%E5%A4%AB%E6%9B%BC%E7%BC%96%E7%A0%81)
  * [树的遍历](https://zh.wikipedia.org/wiki/%E6%A0%91%E7%9A%84%E9%81%8D%E5%8E%86)
  * [最短路径](https://zh.wikipedia.org/wiki/%E6%9C%80%E7%9F%AD%E8%B7%AF%E5%BE%84)算法
  * [最小生成树](https://zh.wikipedia.org/wiki/%E6%9C%80%E5%B0%8F%E7%94%9F%E6%88%90%E6%A0%91)算法
  * [最小树形图](https://zh.wikipedia.org/w/index.php?title=%E6%9C%80%E5%B0%8F%E6%A0%91%E5%BD%A2%E5%9B%BE&action=edit&redlink=1)
  * [网络流](https://zh.wikipedia.org/wiki/%E7%BD%91%E7%BB%9C%E6%B5%81)算法
  * [匹配算法](https://zh.wikipedia.org/w/index.php?title=%E5%8C%B9%E9%85%8D%E7%AE%97%E6%B3%95&action=edit&redlink=1)
  * [分团问题](https://zh.wikipedia.org/wiki/%E5%88%86%E5%9C%98%E5%95%8F%E9%A1%8C)
* [动态规划](https://zh.wikipedia.org/wiki/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)
* [数值分析](https://zh.wikipedia.org/wiki/%E6%95%B0%E5%80%BC%E5%88%86%E6%9E%90)
* [加密算法](https://zh.wikipedia.org/wiki/%E5%8A%A0%E5%AF%86%E7%AE%97%E6%B3%95)
* [排序算法](https://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95)
* [检索](https://zh.wikipedia.org/wiki/%E6%AA%A2%E7%B4%A2)算法
* [随机化算法](https://zh.wikipedia.org/wiki/%E9%9A%8F%E6%9C%BA%E5%8C%96%E7%AE%97%E6%B3%95)
* 关于并行算法，请参阅[并行计算](https://zh.wikipedia.org/wiki/%E5%B9%B6%E8%A1%8C%E8%AE%A1%E7%AE%97)一文。

