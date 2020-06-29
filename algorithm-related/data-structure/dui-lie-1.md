# Queue队列

**队列**，又称为**伫列**（queue），是[先进先出](https://zh.wikipedia.org/wiki/%E5%85%88%E9%80%B2%E5%85%88%E5%87%BA%E6%BC%94%E7%AE%97%E6%B3%95)（FIFO, First-In-First-Out）的[线性表](https://zh.wikipedia.org/wiki/%E7%BA%BF%E6%80%A7%E8%A1%A8)。在具体应用中通常用[链表](https://zh.wikipedia.org/wiki/%E9%93%BE%E8%A1%A8)或者[数组](https://zh.wikipedia.org/wiki/%E6%95%B0%E7%BB%84)来实现。队列只允许在后端（称为rear）进行插入操作，在前端（称为front）进行删除操作。

队列的操作方式和[堆栈](https://zh.wikipedia.org/wiki/%E5%A0%86%E6%A0%88)类似，唯一的区别在于队列只允许新数据在后端进行添加。

#### 单链队列

单链队列使用链表作为基本数据结构，所以不存在伪溢出的问题，队列长度也没有限制。但插入和读取的时间代价较高

```cpp
// 定义单链队列的存储结构
typedef struct QNode {
    int data;
    QNode *next;
}QNode,*QNodePtr;

typedef struct LinkQueue{
    //队头 队尾 指针
    QNodePtr front,rear;
}LinkQueue;


// 构造一个空队列Q
LinkQueue* Q_Init() {
    //申请内存
    LinkQueue* Q = (LinkQueue*)malloc(sizeof(LinkQueue));
    //如果 Q 为 NULL 说明 内存申请失败，结束程序
    if (!Q)
        exit(OVERFLOW);
    //初始化头尾节点 指向相同地址
    Q->front = Q->rear = (QNodePtr)malloc(sizeof(QNode));
    //如果 Q->front 为 NULL 说明 内存申请失败，结束程序
    if (!Q->front)
        exit(OVERFLOW);
    Q->front->next = NULL;
    return Q;
}

// 销毁队列Q(无论空否均可)
void Q_Destroy(LinkQueue *Q) {
    while (Q->front) {
        //将队尾指向队头下一个节点的地址（第1个节点）
        Q->rear = Q->front->next;
        //回收队头
        free(Q->front);
        //将队头指向队尾（相当于第1个节点变成了队头，然后依次第2个第3个、、、
        //直到没有下一个节点，也就是 Q->front == NULL 的时候）
        Q->front = Q->rear;
    }
    free(Q);
}

// 将Q清为空队列
void Q_Clear(LinkQueue *Q) {
    QNodePtr p, q;
    //将队尾指向队头点的地址
    Q->rear = Q->front;
    //取出第1个节点
    p = Q->front->next;
    //回收第1个节点
    Q->front->next = NULL;
    while (p) {
        //将 q 指向 p（第1个节点）
        q = p;
        //将 p 指向 第2个节点
        p = p->next;
        //回收第2个节点
        free(q);
    }
}

// 若Q为空队列，则返回-1，否则返回1
int Q_Empty(LinkQueue Q) {
    if (Q.front->next == NULL)
        return 1;
    else
        return -1;
}

// 求队列的长度
int Q_Length(LinkQueue Q) {
    int i = 0;
    QNodePtr p;
    p = Q.front;
    //遍历队列中的节点，直到队尾等于队头
    while (Q.rear != p) {
        i++;
        p = p->next;
    }
    return i;
}

// 打印队列中的内容
void Q_Print(LinkQueue Q) {
    int i = 0;
    QNodePtr p;
    p = Q.front;
    while (Q.rear != p) {
        i++;
        cout << p->next->data << endl;
        p = p->next;
    }
}

// 若队列不空，则用e返回Q的队头元素，并返回1，否则返回-1
int Q_GetHead(LinkQueue Q, int &e) {
    QNodePtr p;
    if (Q.front == Q.rear)
        return -1;
    p = Q.front->next;
    e = p->data;
    return 1;
}

// 插入元素e为Q的新的队尾元素
void Q_Put(LinkQueue *Q, int e) {
    QNodePtr p = (QNodePtr)malloc(sizeof(QNode));
    if (!p) // 存储分配失败
        exit(OVERFLOW);
    p->data = e;
    p->next = NULL;
    //FIFO，将新节点追加到尾节点后面
    Q->rear->next = p;
    //将新的节点变成尾节点
    Q->rear = p;
}


// 若队列不空，删除Q的队头元素，用e返回其值，并返回1，否则返回-1
int Q_Poll(LinkQueue *Q,int &e) {
    QNodePtr p;
    if (Q->front == Q->rear)
        return -1;
    //取出头节点
    p = Q->front->next;
    //取出头节点的数据
    e = p->data;
    cout << e << endl;
    Q->front->next = p->next;
    if (Q->rear == p)
        Q->rear = Q->front;
    free(p);
    cout << e << endl;
    return 1;
}

```

#### 循环队列

循环队列可以更简单防止伪溢出的发生，但队列大小是固定的。

```cpp
// 队列的顺序存储结构(循环队列)
#define MAX_QSIZE 5 // 最大队列长度+1
typedef struct {
    int *base; // 初始化的动态分配存储空间
    int front; // 头指针，若队列不空，指向队列头元素
    int rear; // 尾指针，若队列不空，指向队列尾元素的下一个位置
} SqQueue;


// 构造一个空队列Q
SqQueue* Q_Init() {
    SqQueue *Q = (SqQueue*)malloc(sizeof(SqQueue));
    // 存储分配失败
    if (!Q){
        exit(OVERFLOW);
    }
    Q->base = (int *)malloc(MAX_QSIZE * sizeof(int));
    // 存储分配失败
    if (!Q->base){
        exit(OVERFLOW);
    }
    Q->front = Q->rear = 0;
    return Q;
}

// 销毁队列Q，Q不再存在
void Q_Destroy(SqQueue *Q) {
    if (Q->base)
        free(Q->base);
    Q->base = NULL;
    Q->front = Q->rear = 0;
    free(Q);
}

// 将Q清为空队列
void Q_Clear(SqQueue *Q) {
    Q->front = Q->rear = 0;
}

// 若队列Q为空队列，则返回1；否则返回-1
int Q_Empty(SqQueue Q) {
    if (Q.front == Q.rear) // 队列空的标志
        return 1;
    else
        return -1;
}

// 返回Q的元素个数，即队列的长度
int Q_Length(SqQueue Q) {
    return (Q.rear - Q.front + MAX_QSIZE) % MAX_QSIZE;
}

// 若队列不空，则用e返回Q的队头元素，并返回OK；否则返回ERROR
int Q_GetHead(SqQueue Q, int &e) {
    if (Q.front == Q.rear) // 队列空
        return -1;
    e = Q.base[Q.front];
    return 1;
}

// 打印队列中的内容
void Q_Print(SqQueue Q) {
    int p = Q.front;
    while (Q.rear != p) {
        cout << Q.base[p] << endl;
        p = (p + 1) % MAX_QSIZE;
    }
}

// 插入元素e为Q的新的队尾元素
int Q_Put(SqQueue *Q, int e) {
    if ((Q->rear + 1) % MAX_QSIZE == Q->front) // 队列满
        return -1;
    Q->base[Q->rear] = e;
    Q->rear = (Q->rear + 1) % MAX_QSIZE;
    return 1;
}

// 若队列不空，则删除Q的队头元素，用e返回其值，并返回1；否则返回-1
int Q_Poll(SqQueue *Q, int &e) {
    if (Q->front == Q->rear) // 队列空
        return -1;
    e = Q->base[Q->front];
    Q->front = (Q->front + 1) % MAX_QSIZE;
    return 1;
}

```

### 阵列队列

```cpp
#define MAX_QSIZE 10 // 最大队列长度+1
// 阵列队列的存储结构
struct Queue {
    int Array[MAX_QSIZE]; // 阵列空间大小
    int front; // 队头
    int rear; // 队尾
    int length; // 队列长度
};

// 构造一个空队列Q
Queue* Q_Init() {
    Queue *Q = (Queue*)malloc(sizeof(Queue));
    if (!Q){
        // 存储分配失败
        exit(OVERFLOW);
    }
    //初始化
    Q->front = Q->rear = Q->length = 0;
    return Q;
}

// 将Q清为空队列
void Q_Clear(Queue *Q) {
    //清除头尾下标和长度
    Q->front = Q->rear = Q->length = 0;
}

// 入列
int Q_Put(Queue *Q, int x) {
    //如果当前元素数量等于最大数量 返回 -1
    if (Q->rear + 1 == MAX_QSIZE) {
        return -1;
    }
    Q->Array[Q->rear] = x;
    Q->rear = Q->rear + 1;
    //length + 1
    Q->length = Q->length + 1;
    return 1;
}

// 出列
int Q_Poll(Queue *Q) {
    //如果当前元素数量等于最大数量 返回 -1
    if (Q->front + 1 == MAX_QSIZE)
        return -1;
    int x = Q->Array[Q->front];
    Q->front = Q->front + 1;
    // 移出后減少1
    Q->length = Q->length - 1;
    return x;
}
```

