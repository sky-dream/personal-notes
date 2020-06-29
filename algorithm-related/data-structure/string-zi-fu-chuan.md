# String字符串

**字符串**（英语：**string**），是由零个或多个[字符](https://zh.wikipedia.org/wiki/%E5%AD%97%E7%AC%A6)组成的有限序列。一般记为 s=a\_{1}a\_{2}\dots a\_{n}}![s=a\_{1}a\_{2}\dots a\_{n}](https://wikimedia.org/api/rest_v1/media/math/render/svg/e29bf631b090323edd6889f810e6cff29538b161)（![0\leq n\lneq \infty ](https://wikimedia.org/api/rest_v1/media/math/render/svg/a24e16ceca183db18fbc18029243b44d668076a7)）。它是[编程语言](https://zh.wikipedia.org/wiki/%E7%BC%96%E7%A8%8B%E8%AF%AD%E8%A8%80)中表示[文本](https://zh.wikipedia.org/wiki/%E6%96%87%E6%9C%AC)的[数据类型](https://zh.wikipedia.org/wiki/%E8%B3%87%E6%96%99%E5%9E%8B%E5%88%A5)。

通常以串的整体作为操作对象，如：在串中查找某个子串、求取一个子串、在串的某个位置上插入一个子串以及删除一个子串等。两个字符串相等的充要条件是：长度相等，并且各个对应位置上的字符都相等。设p、q是两个串，求q在p中首次出现的位置的运算叫做模式匹配。串的两种最基本的存储方式是顺序存储方式和链接存储方式。

### 1. 实现

某些语言如[C++](https://zh.wikipedia.org/wiki/C%2B%2B)把字符串实现为可以用于任何[基本类型](https://zh.wikipedia.org/wiki/%E5%9F%BA%E6%9C%AC%E9%A1%9E%E5%9E%8B)的[模版](https://zh.wikipedia.org/wiki/%E6%B3%9B%E5%9E%8B)，但这是个例外而不是规则。

在一个面向对象语言把字符串表示为对象的情况下，如果值可以在运行期变更，则叫做“可变的”（mutable），如果值在创建后就不可变更了，则叫做“不变的”（immutable）。例如，[Ruby](https://zh.wikipedia.org/wiki/Ruby)有可变字符串，而[Python](https://zh.wikipedia.org/wiki/Python)的字符串是不可变的。

其他语言，最著名的有[Prolog](https://zh.wikipedia.org/wiki/Prolog)和[Erlang](https://zh.wikipedia.org/wiki/Erlang)，避免实现字符串数据类型，转而采用把字符串表示为字符代码的列表的约定。

### 2. 表示法

 一种常用的表示法是使用一个[字符代码](https://zh.wikipedia.org/w/index.php?title=%E5%AD%97%E7%AC%A6%E4%BB%A3%E7%A0%81&action=edit&redlink=1)的[数组](https://zh.wikipedia.org/wiki/%E6%95%B0%E7%BB%84)，每个字符占用一个字节（如在[ASCII](https://zh.wikipedia.org/wiki/ASCII)代码中）或两个字节（如在[unicode](https://zh.wikipedia.org/wiki/Unicode)中）。它的长度可以使用一个结束符（一般是[NUL](https://zh.wikipedia.org/wiki/NUL)，ASCII代码是0，在[C编程语言](https://zh.wikipedia.org/wiki/C%E7%BC%96%E7%A8%8B%E8%AF%AD%E8%A8%80)中使用这种方法）。[\[3\]](https://zh.wikipedia.org/wiki/%E5%AD%97%E7%AC%A6%E4%B8%B2#cite_note-3)或者在前面加入一个[整数](https://zh.wikipedia.org/wiki/%E6%95%B4%E6%95%B0)值来表示它的长度（在[Pascal](https://zh.wikipedia.org/wiki/Pascal)语言中使用这种方法）。

 当然，可能还有其它的表示法。使用[树](https://zh.wikipedia.org/wiki/%E6%A0%91_%28%E5%9B%BE%E8%AE%BA%29)和[列表](https://zh.wikipedia.org/wiki/%E5%88%97%E8%A1%A8)可以使得一些字符串操作（如插入和删除）更高效。

### 3. 算法

这是一些字符串处理[算法](https://zh.wikipedia.org/wiki/%E7%AE%97%E6%B3%95)，在字符串上进行不同的处理：

* [字符串查找算法](https://zh.wikipedia.org/wiki/%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%9F%A5%E6%89%BE%E7%AE%97%E6%B3%95) \[[Knuth–Morris–Pratt算法](https://zh.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt%E7%AE%97%E6%B3%95),......\]
* [排序算法](https://zh.wikipedia.org/wiki/%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95)
* [正则表达式算法](https://zh.wikipedia.org/wiki/%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F)
* [模式匹配](https://zh.wikipedia.org/w/index.php?title=%E6%A8%A1%E5%BC%8F%E5%8C%B9%E9%85%8D&action=edit&redlink=1)

### 4. 相关例题

LeetCode 071, **Simplify Path**， **简化路径** \[Medium\].

LeetCode 443, **String Compression， 压缩字符串** \[Easy\].

LeetCode 012, **Integer to Roman**， **整数转罗马数字** \[Medium\].

