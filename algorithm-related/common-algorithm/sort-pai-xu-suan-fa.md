# Sort 排序算法

### 排序算法列表

#### 稳定的排序

* [冒泡排序](https://zh.wikipedia.org/wiki/%E5%86%92%E6%B3%A1%E6%8E%92%E5%BA%8F)（bubble sort）— ![O\(n^{2}\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392)

```python
import random


def bubble_sort(seq):  # O(n^2), n(n-1)/2 = 1/2(n^2 + n)
    n = len(seq)
    for i in range(n-1):
        print(seq)    # 我打印出来让你看清楚每一轮最高、次高、次次高...的小朋友会冒泡到右边
        for j in range(n-1-i):  # 这里之所以 n-1 还需要 减去 i 是因为每一轮冒泡最大的元素都会冒泡到最后，无需再比较
            if seq[j] > seq[j+1]:
                seq[j], seq[j+1] = seq[j+1], seq[j]
	print(seq)


def test_bubble_sort():
    seq = list(range(10))  # 注意 python3 返回迭代器，所以我都用 list 强转了，python2 range 返回的就是 list
    random.shuffle(seq)   # shuffle inplace 操作，打乱数组
    bubble_sort(seq)
    assert seq == sorted(seq)  # 注意呦，内置的 sorted 就不是 inplace 的，它返回一个新的数组，不影响传入的参数

""" 我打印出来让你看到每次从最高到次高的小盆友就这么排好序了，因为是随机数，你第一个没有排序的数组应该和我的不一样
[3, 4, 5, 0, 9, 1, 7, 8, 6, 2]
[3, 4, 0, 5, 1, 7, 8, 6, 2, 9]
[3, 0, 4, 1, 5, 7, 6, 2, 8, 9]
[0, 3, 1, 4, 5, 6, 2, 7, 8, 9]
[0, 1, 3, 4, 5, 2, 6, 7, 8, 9]
[0, 1, 3, 4, 2, 5, 6, 7, 8, 9]
[0, 1, 3, 2, 4, 5, 6, 7, 8, 9]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
"""
```

* [插入排序](https://zh.wikipedia.org/wiki/%E6%8F%92%E5%85%A5%E6%8E%92%E5%BA%8F)（insertion sort）—![O\(n^{2}\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392)

```python
def insertion_sort(seq):
    """ 每次挑选下一个元素插入已经排序的数组中,初始时已排序数组只有一个元素"""
    n = len(seq)
    print(seq)
    for i in range(1, n):
        value = seq[i]    # 保存当前位置的值，因为转移的过程中它的位置可能被覆盖
        # 找到这个值的合适位置，使得前边的数组有序 [0,i] 有序
        pos = i
        while pos > 0 and value < seq[pos-1]:
            seq[pos] = seq[pos-1]  # 如果前边的元素比它大，就让它一直前移
            pos -= 1
        seq[pos] = value    # 找到了合适的位置赋值就好
        print(seq)


""" 不断把新元素放到已经有序的数组中
[1, 7, 3, 0, 9, 4, 8, 2, 6, 5]
[1, 7, 3, 0, 9, 4, 8, 2, 6, 5]
[1, 3, 7, 0, 9, 4, 8, 2, 6, 5]
[0, 1, 3, 7, 9, 4, 8, 2, 6, 5]
[0, 1, 3, 7, 9, 4, 8, 2, 6, 5]
[0, 1, 3, 4, 7, 9, 8, 2, 6, 5]
[0, 1, 3, 4, 7, 8, 9, 2, 6, 5]
[0, 1, 2, 3, 4, 7, 8, 9, 6, 5]
[0, 1, 2, 3, 4, 6, 7, 8, 9, 5]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
"""
```

* [鸡尾酒排序](https://zh.wikipedia.org/wiki/%E9%B8%A1%E5%B0%BE%E9%85%92%E6%8E%92%E5%BA%8F)（cocktail sort）—![O\(n^{2}\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392)
* [桶排序](https://zh.wikipedia.org/wiki/%E6%A1%B6%E6%8E%92%E5%BA%8F)（bucket sort）—![O\(n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a)；需要![O\(k\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/f5ec39041121b14e8c2b1a986c9b04547b223e3c)额外空间
* [计数排序](https://zh.wikipedia.org/wiki/%E8%AE%A1%E6%95%B0%E6%8E%92%E5%BA%8F)（counting sort）—![O\(n+k\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/cebd2e4442e56daa59f3fab79339f952122c29e8)；需要{![O\(n+k\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/cebd2e4442e56daa59f3fab79339f952122c29e8)额外空间
* [归并排序](https://zh.wikipedia.org/wiki/%E5%BD%92%E5%B9%B6%E6%8E%92%E5%BA%8F)（merge sort）—![O\(n\log n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1)；需要![O\(n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a)额外空间

```python
def merge_sort(seq):
    if len(seq) <= 1:   # 只有一个元素是递归出口
        return seq
    else:
        mid = int(len(seq)/2)
        left_half = merge_sort(seq[:mid])
        right_half = merge_sort(seq[mid:])

        # 合并两个有序的数组
        new_seq = merge_sorted_list(left_half, right_half)
        return new_seq
def merge_sorted_list(sorted_a, sorted_b):
    """ 合并两个有序序列，返回一个新的有序序列

    :param sorted_a:
    :param sorted_b:
    """
    length_a, length_b = len(sorted_a), len(sorted_b)
    a = b = 0
    new_sorted_seq = list()

    while a < length_a and b < length_b:
        if sorted_a[a] < sorted_b[b]:
            new_sorted_seq.append(sorted_a[a])
            a += 1
        else:
            new_sorted_seq.append(sorted_b[b])
            b += 1

    # 最后别忘记把多余的都放到有序数组里
    if a < length_a:
        new_sorted_seq.extend(sorted_a[a:])
    else:
        new_sorted_seq.extend(sorted_b[b:])

    return new_sorted_seq
```

* 原地[归并排序](https://zh.wikipedia.org/wiki/%E5%BD%92%E5%B9%B6%E6%8E%92%E5%BA%8F)— ![O\(n\log^2 n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/48c36489701bc8023db2f8d6bc809b14a7f8dd4e)如果使用最佳的现在版本
* [二叉排序树](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%8F%89%E6%8E%92%E5%BA%8F%E6%A0%91)排序（binary tree sort）— ![O\(n\log n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1)期望时间；![O\(n^{2}\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392)最坏时间；需要![O\(n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a)额外空间
* [鸽巢排序](https://zh.wikipedia.org/wiki/%E9%B8%BD%E5%B7%A2%E6%8E%92%E5%BA%8F)（pigeonhole sort）—![O\(n+k\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/cebd2e4442e56daa59f3fab79339f952122c29e8)；需要![O\(k\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/f5ec39041121b14e8c2b1a986c9b04547b223e3c)额外空间
* [基数排序](https://zh.wikipedia.org/wiki/%E5%9F%BA%E6%95%B0%E6%8E%92%E5%BA%8F)（radix sort）—![{\displaystyle O\(nk\)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/16feb8341ea75a7bb8b3445959360dde7686db10)；需要![O\(n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a)额外空间
* [侏儒排序](https://zh.wikipedia.org/wiki/%E4%BE%8F%E5%84%92%E6%8E%92%E5%BA%8F)（gnome sort）— ![O\(n^{2}\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392)
* [图书馆排序](https://zh.wikipedia.org/wiki/%E5%9B%BE%E4%B9%A6%E9%A6%86%E6%8E%92%E5%BA%8F)（library sort）— ![O\(n\log n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1)期望时间；![O\(n^{2}\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392)最坏时间；需要![{\displaystyle \(1+\varepsilon \)n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0b18535a9414bcc2072d906174ce2d7ae80baeb0)额外空间
* [块排序](https://zh.wikipedia.org/w/index.php?title=%E5%A1%8A%E6%8E%92%E5%BA%8F&action=edit&redlink=1)（block sort）— ![O\(n\log n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1)

#### 不稳定的排序

* [选择排序](https://zh.wikipedia.org/wiki/%E9%81%B8%E6%93%87%E6%8E%92%E5%BA%8F)（selection sort）—![O\(n^{2}\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392)

```python
def select_sort(seq):
    n = len(seq)
    for i in range(n-1):
        min_idx = i    # 我们假设当前下标的元素是最小的
        for j in range(i+1, n):    # 从 i 的后边开始找到最小的元素，得到它的下标
            if seq[j] < seq[min_idx]:
                min_idx = j    # 一个 j 循环下来之后就找到了最小的元素它的下标
        if min_idx != i:    # swap
            seq[i], seq[min_idx] = seq[min_idx], seq[i]


def test_select_sort():
    seq = list(range(10))
    random.shuffle(seq)
    select_sort(seq)
    assert seq == sorted(seq)

"""
[4, 7, 5, 3, 6, 0, 2, 9, 8, 1]
[0, 7, 5, 3, 6, 4, 2, 9, 8, 1]
[0, 1, 5, 3, 6, 4, 2, 9, 8, 7]
[0, 1, 2, 3, 6, 4, 5, 9, 8, 7]
[0, 1, 2, 3, 6, 4, 5, 9, 8, 7]
[0, 1, 2, 3, 4, 6, 5, 9, 8, 7]
[0, 1, 2, 3, 4, 5, 6, 9, 8, 7]
[0, 1, 2, 3, 4, 5, 6, 9, 8, 7]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

"""
```

* [希尔排序](https://zh.wikipedia.org/wiki/%E5%B8%8C%E5%B0%94%E6%8E%92%E5%BA%8F)（shell sort）—![O\(n\log^2 n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/48c36489701bc8023db2f8d6bc809b14a7f8dd4e)如果使用最佳的现在版本
* [克洛弗排序](https://zh.wikipedia.org/w/index.php?title=%E5%85%8B%E6%B4%9B%E5%BC%97%E6%8E%92%E5%BA%8F&action=edit&redlink=1)（Clover sort）—![O\(n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a)期望时间，![O\(n^{2}\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392)最坏情况[\[来源请求\]](https://zh.wikipedia.org/wiki/Wikipedia:%E5%88%97%E6%98%8E%E6%9D%A5%E6%BA%90)
* [梳排序](https://zh.wikipedia.org/wiki/%E6%A2%B3%E6%8E%92%E5%BA%8F)— ![O\(n\log n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1)
* [堆排序](https://zh.wikipedia.org/wiki/%E5%A0%86%E6%8E%92%E5%BA%8F)（heap sort）—![O\(n\log n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1)
* [平滑排序](https://zh.wikipedia.org/w/index.php?title=%E5%B9%B3%E6%BB%91%E6%8E%92%E5%BA%8F&action=edit&redlink=1)（smooth sort）— ![O\(n\log n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1)
* [快速排序](https://zh.wikipedia.org/wiki/%E5%BF%AB%E9%80%9F%E6%8E%92%E5%BA%8F)（quick sort）—![O\(n\log n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1)期望时间，![O\(n^{2}\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392)最坏情况；对于大的、随机数列表一般相信是最快的已知排序

```python
def quicksort_inplace(array, beg, end):    
# 注意这里我们都用左闭右开区间，end 传入 len(array)
    if beg < end:    # beg == end 的时候递归出口
        pivot = partition(array, beg, end)
        quicksort_inplace(array, beg, pivot)
        quicksort_inplace(array, pivot+1, end)
def partition(array, beg, end):
    pivot_index = beg
    pivot = array[pivot_index]
    left = pivot_index + 1
    right = end - 1    # 开区间，最后一个元素位置是 end-1     [0, end-1] or [0: end)，括号表示开区间

    while True:
        # 从左边找到比 pivot 大的
        while left <= right and array[left] < pivot:
            left += 1

        while right >= left and array[right] >= pivot:
            right -= 1

        if left > right:
            break
        else:
            array[left], array[right] = array[right], array[left]

    array[pivot_index], array[right] = array[right], array[pivot_index]
    return right   # 新的 pivot 位置      
```

* [内省排序](https://zh.wikipedia.org/wiki/%E5%86%85%E7%9C%81%E6%8E%92%E5%BA%8F)（introsort）—![O\(n\log n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d2320768fb54880ca4356e61f60eb02a3f9d9f1)
* [耐心排序](https://zh.wikipedia.org/wiki/%E8%80%90%E5%BF%83%E6%8E%92%E5%BA%8F)（patience sort）—![{\displaystyle O\(n\log n+k\)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c9f1b7420b3d24b7300cd5378bafd652f35ef536)最坏情况时间，需要额外的![O\(n+k\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/cebd2e4442e56daa59f3fab79339f952122c29e8)空间，也需要找到[最长的递增子序列](https://zh.wikipedia.org/w/index.php?title=%E6%9C%80%E9%95%B7%E7%9A%84%E9%81%9E%E5%A2%9E%E5%AD%90%E5%BA%8F%E5%88%97&action=edit&redlink=1)（longest increasing subsequence）

#### 不实用的排序

* [Bogo排序](https://zh.wikipedia.org/wiki/Bogo%E6%8E%92%E5%BA%8F)— ![{\displaystyle O\(n\times n!\)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/2baf5437a72d857ecaca6e60a4101f934eb4b94d)，最坏的情况下期望时间为无穷。
* [Stupid排序](https://zh.wikipedia.org/w/index.php?title=Stupid%E6%8E%92%E5%BA%8F&action=edit&redlink=1)—![O\(n^{3}\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/6b04f5c5cfea38f43406d9442387ad28555e2609);递归版本需要![O\(n^{2}\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/6cd9594a16cb898b8f2a2dff9227a385ec183392)额外存储器
* [珠排序](https://zh.wikipedia.org/wiki/%E7%8F%A0%E6%8E%92%E5%BA%8F)（bead sort）— ![O\(n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a) 或 ![O\({\sqrt  {n}}\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/f5526ab1252c0f682bbe07c0ad67c0f29de5522b),但需要特别的硬件
* [煎饼排序](https://zh.wikipedia.org/wiki/%E7%85%8E%E9%A4%85%E6%8E%92%E5%BA%8F)—![O\(n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/34109fe397fdcff370079185bfdb65826cb5565a),但需要特别的硬件
* [臭皮匠排序](https://zh.wikipedia.org/wiki/%E8%87%AD%E7%9A%AE%E5%8C%A0%E6%8E%92%E5%BA%8F)（stooge sort）算法简单，但需要约![{\displaystyle n^{2.7}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0cd84982291be85144f373b0ab62c553a0119c24)的时间

### 简要比较



| 排序算法 | 最差时间分析 | 平均时间复杂度 | 稳定度 | 空间复杂度 |
| :--- | :--- | :--- | :--- | :--- |
| 冒泡排序 | O\(n^2\) | O\(n^2\) | 稳定 | O\(1\) |
| 选择排序 | O\(n^2\) | O\(n^2\) | 不稳定 | O\(1\) |
| 插入排序 | O\(n^2\) | O\(n^2\) | 稳定 | O\(1\) |
| 二叉树排序 | O\(n^2\) | O\(n\*log2n\) | 不一顶 | O\(n\) |
| 快速排序 | O\(n^2\) | O\(n\*log2n\) | 不稳定 | O\(log2n\)~O\(n\) |
| 堆排序 | O\(n\*log2n\) | O\(n\*log2n\) | 不稳定 | O\(1\) |

![](../../.gitbook/assets/pi-zhu-20200423-004403%20%285%29.png)

* 均按从小到大排列
* k代表数值中的"数位"个数
* n代表数据规模
* m代表数据的最大值减最小值



