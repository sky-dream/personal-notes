# c\_cpp

### 存储数据的三块内存区域

堆heap， 有且仅有new出来的对象会存储在堆heap内存中， 

全局数据区， 全局变量，静态本地变量，静态成员变量， 

堆栈stack， 本地变量，在函数内部产生的对象， \(try.catch中 throw抛出的异常exception也存在这，并把堆栈中该异常对象的指针向上返回\) 

代码分区：在使用C/C++编程时，我们定义的变量存在于内存中，而内存在C语言的角度上可以分为五大区。

局部变量在栈区，静态/全局变量在全局区，动态申请的变量存在于堆区，const修饰的变量/字符常量存在于只读区。无论是什么样的变量，终究在内存中。

### c代码优化

* 使用int类型变量，不要使用char，或者short类型，除非需要使用他们的溢出逻辑，否则编译的汇编语言会多增加防溢出语句，降低效率，
* 循环多使用减计数，编译的汇编语句会减少条件判断语句，提高效率，计数器使用无符号数时，结束条件使用i！=0，不要用i＞=0， 
* 至少执行一次的循环多使用while，因为for循环开始前会增加一条条件判断的汇编语句，

### 结构体元素地址对齐

* char，8位， 
* short，16位，
* int，32位，

#### 一般规则

* 将所有8位元素安排在结构体前面，
* 依次安排16位，32位元素，
* 把数组和大元素安排在后面，
* 对于一条语句，如果结构体太大而不能访问其所有元素，可以把元素组织成一个子结构体，编译器可以单独维持其指针，

#### 函数指针

在c语言struct 结构体中定义函数指针元素，该函数指针指向的函数即 相当于 c++类对象的成员函数，

 c++类对象某种程度上类似于c语言中带函数指针的结构体对象的加强版类型，新增了构造函数重载和成员函数重载，类的多态以及继承等等新特性，

实际上c++中是可以使用地址指针避开类的private特性限制来访问对象的private成员变量的，不过这不是好的代码写法，

### C语言和C++语言中的字符串结束符

C语言：字符串以“\0”结束

c++ 里的string一个STL的模板类，C++标准库的string不是以'\0'结束，而是string类中有一个记录长度的值,  string::c\_str\(\)函数返回c字符串也是以'\0'结束,  但是cpp 中仍然可以使用char \[\], 以'\0'为结束标志

```cpp
#include<iostream>
using namespace std;
 
int main()
{
	char str[20] = { 'i','l','o','v','e' };
	char* st = "I love you";
	int a = strlen(str);
	int b = strlen(st);
	int c = sizeof(str);
	int d = sizeof(st);
	return 0;
}

```

{% hint style="info" %}
output: a = 5; b = 10; c = 20; d = 4;
{% endhint %}

 其中 sizeof\(st\)是指针st的大小。

