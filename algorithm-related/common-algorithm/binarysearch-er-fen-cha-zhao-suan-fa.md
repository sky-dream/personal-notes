# BinarySearch二分查找

在[计算机科学](https://zh.wikipedia.org/wiki/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6)中，**二分查找算法**（英语：binary search algorithm），也称**折半搜索算法**（英语：half-interval search algorithm）[\[1\]](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E5%B0%8B%E6%BC%94%E7%AE%97%E6%B3%95#cite_note-1)、**对数搜索算法**（英语：logarithmic search algorithm）[\[2\]](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E5%B0%8B%E6%BC%94%E7%AE%97%E6%B3%95#cite_note-FOOTNOTEKnuth1998%C2%A76.2.1_%28%22Searching_an_ordered_table%22%29,_subsection_%22Binary_search%22-2)，是一种在[有序数组](https://zh.wikipedia.org/wiki/%E6%9C%89%E5%BA%8F%E6%95%B0%E5%AF%B9)中查找某一特定元素的搜索[算法](https://zh.wikipedia.org/wiki/%E7%AE%97%E6%B3%95)。搜索过程从数组的中间元素开始，如果中间元素正好是要查找的元素，则搜索过程结束；如果某一特定元素大于或者小于中间元素，则在数组大于或小于中间元素的那一半中查找，而且跟开始一样从中间元素开始比较。如果在某一步骤数组为空，则代表找不到。这种搜索算法每一次比较都使搜索范围缩小一半。

二分查找算法有许多中变种。比如[分散层叠](https://zh.wikipedia.org/w/index.php?title=%E5%88%86%E6%95%A3%E5%B1%82%E5%8F%A0&action=edit&redlink=1)可以提升在多个数组中对同一个数值的搜索。分散层叠有效的解决了[计算几何学](https://zh.wikipedia.org/wiki/%E8%AE%A1%E7%AE%97%E5%87%A0%E4%BD%95%E5%AD%A6)和其他领域的许多搜索问题。[指数搜索](https://zh.wikipedia.org/w/index.php?title=Exponential_Search&action=edit&redlink=1)将二分查找算法拓宽到无边界的列表。[二叉搜索树](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91)和B树数据结构就是基于[二分查找算法](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE%E7%AE%97%E6%B3%95)的。

## 算法

二分搜索只对有序数组有效。二分搜索先比较数组中比特素和目标值。如果目标值与中比特素相等，则返回其在数组中的位置；如果目标值小于中比特素，则搜索继续在前半部分的数组中进行。如果目标值大于中比特素，则搜索继续在数组上部分进行。由此，算法每次排除掉至少一半的待查数组。

#### 2分搜索的基本条件

* Sorted（单调递增或者递减）
* Bounded（存在上下界）
* Accessible by index（能够通过索引访问）

#### 拓展的使用场景------大致匹配

以上描述只适用于完全匹配，也就是查找一个目标值的位置。不过，因为有序数组的顺序性，将二分搜索算法扩展到能适用大致匹配并不是很重要。举例来说，二分搜索算法可以用来计算一个赋值的**排名**（或称**秩**，比它更小的元素的数量）、**前趋**（下一个最小元素）、**后继**（下一个最大元素）以及[**最近邻**](https://zh.wikipedia.org/wiki/%E6%9C%80%E9%84%B0%E8%BF%91%E6%90%9C%E7%B4%A2)。查找两个值之间的元素数目的[范围查询](https://zh.wikipedia.org/w/index.php?title=%E7%AF%84%E5%9C%8D%E6%9F%A5%E8%A9%A2_%28%E8%B3%87%E6%96%99%E7%B5%90%E6%A7%8B%29&action=edit&redlink=1)可以借由两个[排名查询](https://zh.wikipedia.org/w/index.php?title=%E6%8E%92%E5%90%8D%E6%9F%A5%E8%A9%A2&action=edit&redlink=1)（又称**秩查询**）来运行[\[5\]](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E5%B0%8B%E6%BC%94%E7%AE%97%E6%B3%95#cite_note-FOOTNOTESedgewickWayne2011%C2%A73.1,_subsection_%22Rank_and_selection%22-5)。

### 示例代码

#### C 版本- 递归

```c
int binary_search(const int arr[], int start, int end, int khey) {
	if (start > end)
		return -1;

	int mid = start + (end - start) / 2;    //直接平均可能會溢位，所以用此算法
	if (arr[mid] > khey)
		return binary_search(arr, start, mid - 1, khey);
	else if (arr[mid] < khey)
		return binary_search(arr, mid + 1, end, khey);
	else
	    return mid;        //最後檢測相等是因為多數搜尋狀況不是大於要不就小於
}
```

#### C 版本- while 循环

```c
int binary_search(const int arr[], int start, int end, int key) {
    int ret = -1;       // 未搜索到数据返回-1下标
    
	int mid;
	while (start <= end) {
		mid = start + (end - start) / 2; //直接平均可能會溢位，所以用此算法
		if (arr[mid] < key)
			start = mid + 1;
		else if (arr[mid] > key)
			end = mid - 1;
		else {            // 最後檢測相等是因為多數搜尋狀況不是大於要不就小於
			ret = mid;  
            break;
        }
	}
	
	return ret;     // 单一出口
}
```

#### Python3 版本 while 循环

```python
def binary_search(arr, left, right, hkey):
    while left <= right:
        mid = left + (right - left) // 2
        if arr[mid] == hkey:
            return mid
        elif arr[mid] < hkey:
            left = mid + 1
        elif arr[mid] > hkey:
            right = mid - 1
    return -1
```

#### Python3 版本 递归

```python
def binary_search(arr, start, end, hkey):
	if start > end:
		return -1
	mid = start + (end - start) / 2
	if arr[mid] > hkey:
		return binary_search(arr, start, mid - 1, hkey)
	if arr[mid] < hkey:
		return binary_search(arr, mid + 1, end, hkey)
	return mid
```

### 实现中的问题

> 尽管二分查找的基本思想相对简单，但细节可以令人难以招架 ... — [高德纳](https://zh.wikipedia.org/wiki/%E9%AB%98%E5%BE%B7%E7%BA%B3)

当[乔恩·本特利](https://zh.wikipedia.org/w/index.php?title=%E4%B9%94%E6%81%A9%C2%B7%E6%9C%AC%E7%89%B9%E5%88%A9&action=edit&redlink=1)将二分搜索问题布置给专业编程课的学生时，百分之90的学生在花费数小时后还是无法给出正确的解答，主要因为这些错误程序在面对边界值的时候无法运行，或返回错误结果。1988年开展的一项研究显示，20本教科书里只有5本正确实现了二分搜索。不仅如此，本特利自己1986年出版的《编程珠玑》一书中的二分搜索算法存在整数溢出的问题，二十多年来无人发现。[Java语言](https://zh.wikipedia.org/wiki/Java)的库所实现的二分搜索算法中同样的溢出问题存在了九年多才被修复。

### 相关例题

LeetCode 074, **Search a 2D Matrix，** **搜索二维矩阵** \[Medium\].

LeetCode 287, **Find the Duplicate Number，** **寻找重复数** \[Medium\].

LeetCode 719, **Find K-th Smallest Pair Distance，** **找出第 k 小的距离对** \[Hard\].

LeetCode 153, **Find Minimum in Rotated Sorted Array，** **寻找旋转排序数组中的最小值** \[Medium\].

LeetCode 1095, **Find in Mountain Array，** **山脉数组中查找目标值** \[Hard\].

