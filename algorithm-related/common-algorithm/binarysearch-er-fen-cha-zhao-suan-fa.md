# BinarySearch二分查找算法

在[计算机科学](https://zh.wikipedia.org/wiki/%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6)中，**二分查找算法**（英语：binary search algorithm），也称**折半搜索算法**（英语：half-interval search algorithm）[\[1\]](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E5%B0%8B%E6%BC%94%E7%AE%97%E6%B3%95#cite_note-1)、**对数搜索算法**（英语：logarithmic search algorithm）[\[2\]](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E5%B0%8B%E6%BC%94%E7%AE%97%E6%B3%95#cite_note-FOOTNOTEKnuth1998%C2%A76.2.1_%28%22Searching_an_ordered_table%22%29,_subsection_%22Binary_search%22-2)，是一种在[有序数组](https://zh.wikipedia.org/wiki/%E6%9C%89%E5%BA%8F%E6%95%B0%E5%AF%B9)中查找某一特定元素的搜索[算法](https://zh.wikipedia.org/wiki/%E7%AE%97%E6%B3%95)。搜索过程从数组的中间元素开始，如果中间元素正好是要查找的元素，则搜索过程结束；如果某一特定元素大于或者小于中间元素，则在数组大于或小于中间元素的那一半中查找，而且跟开始一样从中间元素开始比较。如果在某一步骤数组为空，则代表找不到。这种搜索算法每一次比较都使搜索范围缩小一半。

二分查找算法在情况下的复杂度是对数时间，进行![O\(\log n\)](https://wikimedia.org/api/rest_v1/media/math/render/svg/aae0f22048ba6b7c05dbae17b056bfa16e21807d)次比较操作![n](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b)在此处是数组的元素数量，![O](https://wikimedia.org/api/rest_v1/media/math/render/svg/9d70e1d0d87e2ef1092ea1ffe2923d9933ff18fc)是[大O记号](https://zh.wikipedia.org/wiki/%E5%A4%A7O%E7%AC%A6%E5%8F%B7)，![\log ](https://wikimedia.org/api/rest_v1/media/math/render/svg/79e4debd0ab1c6ce342d0172a7643733305c37bc)是[对数](https://zh.wikipedia.org/wiki/%E5%AF%B9%E6%95%B0)）。二分查找算法使用常数空间，无论对任何大小的输入数据，算法使用的空间都是一样的。除非输入数据数量很少，否则二分查找算法比线性搜索更快，但数组必须事先被排序。尽管特定的、为了快速搜索而设计的数据结构更有效（比如[哈希表](https://zh.wikipedia.org/wiki/%E5%93%88%E5%B8%8C%E8%A1%A8)），二分查找算法应用面更广。

二分查找算法有许多中变种。比如[分散层叠](https://zh.wikipedia.org/w/index.php?title=%E5%88%86%E6%95%A3%E5%B1%82%E5%8F%A0&action=edit&redlink=1)可以提升在多个数组中对同一个数值的搜索。分散层叠有效的解决了[计算几何学](https://zh.wikipedia.org/wiki/%E8%AE%A1%E7%AE%97%E5%87%A0%E4%BD%95%E5%AD%A6)和其他领域的许多搜索问题。[指数搜索](https://zh.wikipedia.org/w/index.php?title=Exponential_Search&action=edit&redlink=1)将二分查找算法拓宽到无边界的列表。[二叉搜索树](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91)和B树数据结构就是基于[二分查找算法](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE%E7%AE%97%E6%B3%95)的。

## 算法

二分搜索只对有序数组有效。二分搜索先比较数组中比特素和目标值。如果目标值与中比特素相等，则返回其在数组中的位置；如果目标值小于中比特素，则搜索继续在前半部分的数组中进行。如果目标值大于中比特素，则搜索继续在数组上部分进行。由此，算法每次排除掉至少一半的待查数组。

#### 步骤

给予一个包含![n](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b)个带值元素的数组![A](https://wikimedia.org/api/rest_v1/media/math/render/svg/7daff47fa58cdfd29dc333def748ff5fa4c923e3)或是[记录](https://zh.wikipedia.org/wiki/%E8%AE%B0%E5%BD%95) ![{\displaystyle A\_{0},\cdots ,A\_{n-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/919c30b8cf5a22c8d6fa2a5b08450d71d9048d48)，使![{\displaystyle A\_{0}\leq \cdots \leq A\_{n-1}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/8041fd82c778dc6e84c8a9e8f7e4fd16d3af8117)，以及目标值![T](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0)，还有下列用来查找![T](https://wikimedia.org/api/rest_v1/media/math/render/svg/ec7200acd984a1d3a3d7dc455e262fbe54f7f6e0)在![A](https://wikimedia.org/api/rest_v1/media/math/render/svg/7daff47fa58cdfd29dc333def748ff5fa4c923e3)中位置的[子程序](https://zh.wikipedia.org/wiki/%E5%AD%90%E7%A8%8B%E5%BC%8F)[\[3\]](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E5%B0%8B%E6%BC%94%E7%AE%97%E6%B3%95#cite_note-FOOTNOTEKnuth1998%C2%A76.2.1_%28%22Searching_an_ordered_table%22%29,_subsection_%22Algorithm_B%22-3)。

1. 令![L](https://wikimedia.org/api/rest_v1/media/math/render/svg/103168b86f781fe6e9a4a87b8ea1cebe0ad4ede8)为![{\displaystyle  0 }](https://wikimedia.org/api/rest_v1/media/math/render/svg/2aae8864a3c1fec9585261791a809ddec1489950)，![R](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33)为![{\displaystyle n-1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/fbd0b0f32b28f51962943ee9ede4fb34198a2521)。
2. 如果![{\displaystyle L&amp;gt;R}](https://wikimedia.org/api/rest_v1/media/math/render/svg/145ce1d631364a50d19ac5264c7dc09d4e158b0a)，则查找以失败告终。
3. 令![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc)（中间值元素）为![{\displaystyle \lfloor \(L+R\)/2\rfloor }](https://wikimedia.org/api/rest_v1/media/math/render/svg/ed16e26ee115a08516277e94cfe5c898b19f7094)。（具体实现中，为防止[算术溢出](https://zh.wikipedia.org/wiki/%E7%AE%97%E8%A1%93%E6%BA%A2%E5%87%BA)，一般采用![{\displaystyle \lfloor L+\(R-L\)/2\rfloor }](https://wikimedia.org/api/rest_v1/media/math/render/svg/de072f6957d10f5935bb05b30b39580753b4dbe6)代替。）
4. 如果![{\displaystyle A\_{m}&amp;lt;T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/3f302eb8600e5c6930a74778a3232e4a1c8d91bc)，令![L](https://wikimedia.org/api/rest_v1/media/math/render/svg/103168b86f781fe6e9a4a87b8ea1cebe0ad4ede8)为![{\displaystyle m+1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c6f7ed29a2b4a62d3b6af05cd91a58ffc6094201)并回到步骤二。
5. 如果![{\displaystyle A\_{m}&amp;gt;T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/d8f333a047adf793929566dda96ffdf4493cf3b7)，令![R](https://wikimedia.org/api/rest_v1/media/math/render/svg/4b0bfb3769bf24d80e15374dc37b0441e2616e33)为![{\displaystyle m-1}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ecbbd201e0d8f1ccc91cb46362c4b72fa1bbe6c2)并回到步骤二。
6. 当![{\displaystyle A\_{m}=T}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0e65e98f38acc1a2a6e07c43495b3a0058255c6d)，查找结束；回传值![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc)。

这个[迭代](https://zh.wikipedia.org/wiki/%E7%96%8A%E4%BB%A3)步骤会持续透过两个变量追踪搜索的边界。有些实际应用会在算法的最后放入相等比较，让比较循环更快，但平均而言会多一层迭代[\[4\]](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E5%B0%8B%E6%BC%94%E7%AE%97%E6%B3%95#cite_note-bottenbruch-4)。

#### 大致匹配

以上程序只适用于完全匹配，也就是查找一个目标值的位置。不过，因为有序数组的顺序性，将二分搜索算法扩展到能适用大致匹配并不是很重要。举例来说，二分搜索算法可以用来计算一个赋值的**排名**（或称**秩**，比它更小的元素的数量）、**前趋**（下一个最小元素）、**后继**（下一个最大元素）以及[**最近邻**](https://zh.wikipedia.org/wiki/%E6%9C%80%E9%84%B0%E8%BF%91%E6%90%9C%E7%B4%A2)。查找两个值之间的元素数目的[范围查询](https://zh.wikipedia.org/w/index.php?title=%E7%AF%84%E5%9C%8D%E6%9F%A5%E8%A9%A2_%28%E8%B3%87%E6%96%99%E7%B5%90%E6%A7%8B%29&action=edit&redlink=1)可以借由两个[排名查询](https://zh.wikipedia.org/w/index.php?title=%E6%8E%92%E5%90%8D%E6%9F%A5%E8%A9%A2&action=edit&redlink=1)（又称**秩查询**）来运行[\[5\]](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E5%B0%8B%E6%BC%94%E7%AE%97%E6%B3%95#cite_note-FOOTNOTESedgewickWayne2011%C2%A73.1,_subsection_%22Rank_and_selection%22-5)。

* 排名查询可以使用调整版的二分搜索来运行。借由在成功的搜索回传![{\displaystyle m}](https://wikimedia.org/api/rest_v1/media/math/render/svg/0a07d98bb302f3856cbabc47b2b9016692e3f7bc)，以及在失败的搜索回传![L](https://wikimedia.org/api/rest_v1/media/math/render/svg/103168b86f781fe6e9a4a87b8ea1cebe0ad4ede8)，就会取而代之地回传了比起目标值小的元素数目[\[5\]](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E5%B0%8B%E6%BC%94%E7%AE%97%E6%B3%95#cite_note-FOOTNOTESedgewickWayne2011%C2%A73.1,_subsection_%22Rank_and_selection%22-5)。
* 前趋和后继查询可以借由排名查询来运行。一旦知道目标值的排名，其前趋就会是那个位于其排名位置的元素,或者排名位置的上一个元素（因为它是小于目标值的最大元素）。其后继是（数组中的）下一个元素，或是（非数组中的）前趋的下一个元素[\[6\]](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E5%B0%8B%E6%BC%94%E7%AE%97%E6%B3%95#cite_note-FOOTNOTEGoldmanGoldman2008461%E2%80%93463-6)。目标值的最近邻可能是前趋或后继，取决于何者较为接近。
* 范围查询也是直接了当的。一旦知道两个值的排名，不小于第一个值且小于第二个值的元素数量就会是两者排名的差。这个值可以根据范围的端点是否算在范围内，或是数组是否包含其端点的对应键来增加或减少1[\[7\]](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%88%86%E6%90%9C%E5%B0%8B%E6%BC%94%E7%AE%97%E6%B3%95#cite_note-FOOTNOTESedgewickWayne2011%C2%A73.1,_subsection_%22Range_queries%22-7)。

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

