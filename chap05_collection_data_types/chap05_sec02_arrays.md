
### 5.2. 数组
> 什么是数组？数组是由一组有序数据元素组合成的数据类型，其中所有元素都是相同的类型，你可以通过索引来访问元素值。说的更精确些，数组一组有序数值存储在连续的计算机内存区域中，每个元素之间都具有相同的地址间隔。
>
> 注意，C++ 中的数组总是存储在连续的内存区域中。数组可由以下两种方式声明：
> 1. *静态分配*：数组大小在编译时已经确定，且不能改变
> 2. *动态分配*：分配时涉及指针的使用，其大小在运行时能够被改变

> 在现代 C++ 里，静态分配的数组一般用在对速度或硬件要求十分苛刻的环境下。能够动态分配的向量 <small>(vector)</small> 则用于你特别需要很多灵活性的情况。
>
> 作为一名 Python 开发者，你可能会将 C++ 里的数组 <small>(array)</small> 看作是 Python 中 list 的鼻祖，Python 的 list 的内部实现确实是由数组编写，唯一的不同只是 list 中存储的是引用而非值。
>
> 两者非常相似，比如它们都是以 `0` 作为索引的开头。其差异包含有：C++ 的每个元素处能够直接存储值，Python 则是引用；C++ 数组中的每个元素必须是同样的数据类型，Python 则没有此类限制。
>
> 数组使我们能够将一组有序且连续的内存作为一个整体来操作，同时我们仍然能够访问特定单个元素。

> **为什么要使用数组？**
>
> C++ 语言通常用于实时处理，或是对速度要求非常严格的底层操作，以及两者在内存空间十分有限的情况下。
>
> 因为数组中每个元素都存在连续的位置上，其查找速度会非常非常快。在计算领域中，一个 *word* 为特定处理器设计下 <small>(比如 *32* 或 *64* 位)</small> 数据的单位。假设我们有一个含 100 个整数元素的数组，它们可能分别存储在内存地址 `20000`、`20004`、`20008` ... `20396`。索引 `i` 处的元素即应处于 `20000 + 4 x i` 内存地址处。

> 静态分配的 C++ 数组在声明时就必须指明其大小和类型:
```cpp
double dArr[420];
int    iArr[42];
char   cArr[4];
```

> 当然，你也可以直接初始化数组，编译器能够自动由元素数量判断其大小：
```cpp
int arr[]     = {1, 2, 3, 4};                   // size: 4
char arr2[]   = {'a', 'b', 'c'};                // size: 3
string arr3[] = {"this", "is", "an", "array"};  // size: 4
```

> 注意：单个元素数组中的元素与相对的原子数据类型完全不一样，故以下两者是不一样的：
```cpp
double dArr[] = { 1.2 };    // must via index, i.e. dArr[0]
double dDbl   =   1.2  ;    // access directly
```

> **用数组时小心这些事**
>
> C++ 数组给我们带来的速度与对底层的控制是把双刃剑。作为一名 Python 开发者，使用过后你就能大致明白不同实现的取舍了。
```cpp
#include <iostream>
using namespace std;

int main() {
    int myarray[] = { 2, 4, 6, 8 };

    for (int i = 0; i < 4; i++){
        cout << myarray[i] << endl;
    }
    return 0;
}

```
>
> 在 Python 里循环一旦越界就会立即报错：
```python
def main():
    mylist = [2, 4, 6, 8]

    for i in range(8):
        print(mylist[i])

main()
```

> Python 提供的保护在 C++ 里需要来用速度来交换。Python 绝对不会让你的循环越过列表末尾，C++ 则不然，你不仅可以访问超出当前列表的元素，你甚至还能够改变它们的值，操作不当这将导致灾难性的后果。
>
> 有这样一句话：*be careful what you wish for*（近似 *叶公好龙* 的意思），在用在 C++ 里再贴切不过了。你说什么，C++ 就会做什么：
```cpp
#include <iostream>
using namespace std;

int main() {
    int myarray[] = {2,4,6,8};
    for (int i = 0; i <= 8; i++){
        cout << myarray[i] << endl;
        cout << "id: " << &myarray[i] << endl;
    }
    return 0;
}
```
>
> Python 对越界访问有一定的保护，一旦越界便会立即报错：
```python
def main():
    mylist = [2,4,6,8]
    print(mylist)

    for i in range(5):
        print(mylist[i])
        print(f"id: {str(id(mylist[i]))}")

main()
```

> C++ 的快并不是没有取舍，其中之一即是错误检查。
>
> 你当然应该用数组，特别是在速度或硬件要求十分苛刻的情况下。但除此以外，你可能更想使用更灵活的向量集合数据类型。
```cpp
#include <iostream>
using namespace std;

int main() {
    int myarray[]   = {2, 4};
    int otherdata[] = {777, 777};

    for (int i = 0; i < 4; i++){
        myarray[i] = 0;
        cout << "myarray[" << i << "]=";
        cout << myarray[i] << endl;
        cout << "add:"     << &myarray[i] << endl;
    }

    for (int i = 0; i < 2; i++){
        cout << "otherdata[" << i << "]=";
        cout << otherdata[i] << endl;
        cout << "add:"       << &otherdata[i] << endl;
    }

    return 0;
}
```
>
> Python 对越界访问有一定的保护，故以下第二个数组的值完全不会被影响：
```python
def main():
    mylist    = [2, 4]
    otherdata = [777, 777]

    for i in range(4):
        print(mylist[i])
        print(f"id: {str(id(mylist[i]))}")

    for j in range(2):
        print(otherdata[i])
        print(f"id: {str(id(otherdata[i]))}")

main()
```

> 在以上代码中，`otherdata[]` 中的数值为何与预期大相径庭？（单选）
>
> 1. 没问题
> 2. 所有的数据被重新初始化了
> 3. 我也不明白，能提示下吗
> 4. 头一个循环越界了，其写操作覆盖了 `otherdata[]` 中的数据
> 5. 以上都不是
>
> 哪种声明数组的方式是正确的？（单选）
>
> 1. `int myarray(5);`
> 2. `myarray[5];`
> 3. `int myarray[5];`
> 4. 以上都不是
