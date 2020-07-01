# UnionFind并查集

并查集 \(union & find\) 是⼀一种树型的数据结构，用于处理一些 不交 集（Disjoint Sets）的合并及查询问题。 

* Find：确定元素属于哪⼀一个⼦子集。它可以被⽤用来确定两个元素是否 属于同⼀一⼦子集。 
* Union：将两个⼦子集合并成同⼀一个集合。

由于支持这两种操作，一个不相交集也常被称为联合-查找数据结构（union-find data structure）或合并-查找集合（merge-find set）。其他的重要方法，`MakeSet`，用于创建单元素集合。有了这些方法，许多经典的划分问题可以被解决。

为了更加精确的定义这些方法，需要定义如何表示集合。一种常用的策略是为每个集合选定一个固定的元素，称为代表，以表示整个集合。接着，`Find(x)` 返回`x`所属集合的代表，而`Union`使用两个集合的代表作为参数。

### 1. 并查集森林

**并查集森林**是一种将每一个集合以树表示的数据结构，其中每一个节点保存着到它的父节点的引用（见意大利面条堆栈）。这个数据结构最早由Bernard A. Galler和Michael J. Fischer于1964年提出，\[1\]但是经过了数年才完成了精确的分析。

在并查集森林中，每个集合的代表即是集合的根节点。“查找”根据其父节点的引用向根行进直到到底树根。“联合”将两棵树合并到一起，这通过将一棵树的根连接到另一棵树的根。

```javascript
function MakeSet(x)
     x.parent := x
 function Find(x)
     if x.parent == x
        return x
     else
        return Find(x.parent)
 function Union(x, y)
     xRoot := Find(x)
     yRoot := Find(y)
     xRoot.parent := yRoot
```

### 2. 主要操作

#### 2.1 合并两个不相交集合

```c
void Union(int x,int y)
{
    fx = getfather(x);
    fy = getfather(y);
    if(fy!=fx)
       father[fx]=fy;
}
```

#### 2.2 判断两个元素是否属于同一集合

```c
bool same(int x,int y)
{
   return getfather(x)==getfather(y);
}
/*返回true 表示相同根结点，返回false不相同*/
```

### 3. 并查集的优化

#### 3.1 路径压缩

刚才我们说过，寻找祖先时采用递归，但是一旦元素一多起来，或退化成一条链，每次`GetFather`都将会使用![O\(n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a)的复杂度，这显然不是我们想要的。

对此，我们必须要进行路径压缩，即我们找到最久远的祖先时“顺便”把它的子孙直接连接到它上面。这就是路径压缩了。使用路径压缩的代码如下：

```c
int getfather(int v)
{
    if (father[v]==v)
      return v;
    else
    {
        father[v]=getfather(father[v]);//路径压缩
        return father[v];
     }
}
```

#### 3.2 Rank合并

合并时将元素所在深度小的集合合并到元素所在深度大的集合。

```c
void judge(int x ,int y)

{
     fx = getfather(x);
     fy = getfather(y);

     if (rank[fx]>rank[fy])
        father[fy] = fx;
     else
     {
        father[fx] = fy;
        if(rank[fx]==rank[fy])
           ++rank[fy]; //重要的是祖先的rank，所以只用修改祖先的rank就可以了，子节点的rank不用管
     }
}
//初始化
memset(rank,0,sizeof(rank));
```

### 4. 时间及空间复杂度

 时间复杂度，   同时使用路径压缩、按秩（rank）合并优化的程序每个操作的平均时间仅为![O\(\alpha \(n\)\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/0f2f9c5bf5571b12dd0907f0a1ef917e1c082201)，其中 ![\alpha \(n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/74c1642d9e2f86b9e5c86c0f18ee5377507da827) 是![{\displaystyle n=f\(x\)=A\(x,x\)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/5bcc6ab1771bb643699c39ff45998c876e788261) 的反函数，![A](https://wikimedia.org/api/rest_v1/media/math/render/svg/7daff47fa58cdfd29dc333def748ff5fa4c923e3) 是急速增加的[阿克曼函数](https://zh.wikipedia.org/wiki/%E9%98%BF%E5%85%8B%E6%9B%BC%E5%87%BD%E6%95%B0)。因为 ![\alpha \(n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/74c1642d9e2f86b9e5c86c0f18ee5377507da827) 是其反函数，故 ![\alpha \(n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/74c1642d9e2f86b9e5c86c0f18ee5377507da827) 在![n](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b) 十分巨大时还是小于![5](https://wikimedia.org/api/rest_v1/media/math/render/svg/29483407999b8763f0ea335cf715a6a5e809f44b)。因此，平均运行时间是一个极小的常数。实际上，这是渐近最优算法：Fredman 和 Saks 在 1989 年解释了![\Omega \(\alpha \(n\)\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/9bfdfd41667be083aff4b7c292a9f35884b654b8) 的平均时间内可以获得任何并查集。

空间复杂度 ， ![O\(n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a)（![n](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b)为元素数量）

### 5. 相关例题

LeetCode 200, Number\_of\_Islands， 岛屿数量 \[Medium\].

LeetCode 547, Friend\_Circles， 朋友圈 \[Medium\].

LeetCode 685, Redundant\_Connection\_II，冗余连接 II \[Hard\].

LeetCode 1049, Last Stone Weight II， 最后一块石头的重量 II \[Medium\].

LeetCode 128, Longest Consecutive Sequence， 最长连续序列 \[Hard\].



