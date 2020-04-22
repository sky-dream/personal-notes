# DFS深度优先搜索

## 定义

**深度优先搜索算法**（英语：Depth-First-Search，DFS）是一种用于遍历或搜索[树](https://zh.wikipedia.org/wiki/%E6%A0%91_%28%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%29)或[图](https://zh.wikipedia.org/wiki/%E5%9B%BE_%28%E6%95%B0%E5%AD%A6%29)的[算法](https://zh.wikipedia.org/wiki/%E7%AE%97%E6%B3%95)。这个算法会尽可能深的搜索树的分支。当节点v的所在边都己被探寻过，搜索将回溯到发现节点v的那条边的起始节点。这一过程一直进行到已发现从源节点可达的所有节点为止。如果还存在未被发现的节点，则选择其中一个作为源节点并重复以上过程，整个进程反复进行直到所有节点都被访问为止。这种算法不会根据图的结构等信息调整执行策略。

深度优先搜索是图论中的经典算法，利用深度优先搜索算法可以产生目标图的[拓扑排序](https://zh.wikipedia.org/wiki/%E6%8B%93%E6%89%91%E6%8E%92%E5%BA%8F)表，利用拓扑排序表可以方便的解决很多相关的[图论](https://zh.wikipedia.org/wiki/%E5%9B%BE%E8%AE%BA)问题，如无权最长路径问题等等。

 因发明“深度优先搜索算法”，[约翰·霍普克洛夫特](https://zh.wikipedia.org/wiki/%E7%B4%84%E7%BF%B0%C2%B7%E9%9C%8D%E6%99%AE%E5%85%8B%E6%B4%9B%E5%A4%AB%E7%89%B9)与[罗伯特·塔扬](https://zh.wikipedia.org/wiki/%E7%BD%97%E4%BC%AF%E7%89%B9%C2%B7%E5%A1%94%E6%89%AC)在[1986年](https://zh.wikipedia.org/wiki/1986%E5%B9%B4)共同获得计算机领域的最高奖：[图灵奖](https://zh.wikipedia.org/wiki/%E5%9B%BE%E7%81%B5%E5%A5%96)。

### 实现方法

1. 首先将根节点放入stack中。
2. 从stack中取出第一个节点，并检验它是否为目标。如果找到目标，则结束搜寻并回传结果。否则将它某一个尚未检验过的直接子节点加入stack中。
3. 重复步骤2。
4. 如果不存在未检测过的直接子节点。将上一级节点加入stack中。重复步骤2。
5. 重复步骤4。
6. 若stack为空，表示整张图都检查过了——亦即图中没有欲搜寻的目标。结束搜寻并回传“找不到目标”。

## C++的实现

 定义一个结构体来表达一个二叉树的[节点](https://zh.wikipedia.org/wiki/%E8%8A%82%E7%82%B9)的结构：



```cpp
struct Node {
2     int self;     // 數據
3     Node *left;   // 左節點
4     Node *right;  // 右節點
5 };
```

 通过使用[C++](https://zh.wikipedia.org/wiki/C%2B%2B)的[STL](https://zh.wikipedia.org/wiki/STL)，下面的程序能帮助理解：

```cpp
const int TREE_SIZE = 9;
std::stack<Node *> unvisited;
Node nodes[TREE_SIZE];
Node *current;

//初始化樹
for (int i = 0; i < TREE_SIZE; i++) {
    nodes[i].self = i;
    int child = i * 2 + 1;
    if (child < TREE_SIZE) // Left child
        nodes[i].left = &nodes[child];
    else
        nodes[i].left = NULL;
    child++;
    if (child < TREE_SIZE) // Right child
        nodes[i].right = &nodes[child];
    else
        nodes[i].right = NULL;
}

unvisited.push(&nodes[0]); //先把0放入UNVISITED stack

// 樹的深度優先搜索在二叉樹的特例下，就是二叉樹的先序遍歷操作（這裡是使用循環實現)
// 只有UNVISITED不空
while (!unvisited.empty()) {
    current = (unvisited.top()); //當前應該訪問的
    unvisited.pop();
    if (current->right != NULL)
        unvisited.push(current->right );
    if (current->left != NULL)
        unvisited.push(current->left);
    cout << current->self << endl;
}
```

