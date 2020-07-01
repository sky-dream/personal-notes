# Stack堆栈

**堆栈**（英语：stack）又称为**栈**或**堆叠**，是计算机科学中的一种抽象数据类型，只允许在有序的线性数据集合的一端（称为堆栈顶端，英语：top）进行加入数据（英语：push）和移除数据（英语：pop）的运算。因而按照后进先出（LIFO, Last In First Out）的原理运作。

常与另一种有序的线性数据集合队列相提并论。

堆栈常用一维数组或链表来实现。

### 1. 操作

堆栈使用两种基本操作：推入（压栈，push）和弹出（弹栈，pop）：

* 推入：将数据放入堆栈顶端，堆栈顶端移到新放入的数据。
* 弹出：将堆栈顶端数据移除，堆栈顶端移到移除后的下一笔数据。

### 2. 特点

堆栈的基本特点：

1. 先入后出，后入先出。
2. 除头尾节点之外，每个元素有一个前驱，一个后继。

### 3. 相关例题

LeetCode 071, **Simplify Path**， **简化路径** \[Medium\].

LeetCode 173, **Binary Search Tree Iterator**， **二叉搜索树迭代器** \[Medium\].

LeetCode 402, **Remove K Digits**， **移掉K位数字** \[Medium\].

LeetCode 155, **Min Stack**， **最小栈 \[Easy\]**.

LeetCode 591, **Tag Validator**， **标签验证器 \[Hard\]**.

LeetCode 772, **Basic Calculator III**， **基本计算器 III \[Hard\]**.

LeetCode 232, **Implement Queue using Stacks**， **用栈实现队列 \[Easy\]**.

LeetCode 225, **Implement Stack using Queues**， **用队列实现栈** **\[Easy\]**.

