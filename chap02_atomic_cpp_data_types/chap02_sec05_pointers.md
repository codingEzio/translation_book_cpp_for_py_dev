
### 2.5. 指针
> 在 C++ 里，指针用于存储内存地址，并且可以间接地访问那个地址上的数据。

> 让我们来看下这两个语言是如何存储一个整数的（示例）。
>
> 在 Python 里，所有的东西都以对象存储。Python 里的变量只是存储了一个引用，其指向内存中那个对象的地址。因此，每个 Python 变量实际上需要两个内存地址：一个是引用即对象的地址，另一个是以对象存在的实际的数值。
>
> 在 C++ 里，每个变量直接存储在内存中，并不需要引用或是对象来存。这样做访问起来很快，这也是为什么每次我们要给变量指定类型，提前分配好每个变量能占用的空间。

> Python 图示
    >> `varN = 100`
    >> <img src="../_images/chap02_sec05_reference_python.png" height="auto" width="50%" margin="auto" alt="Python Reference">

> C++ 图示
    >> `int varN = 100;`
    >> <img src="../_images/chap02_sec05_reference_cpp.png" height="auto" width="50%" margin="auto" alt="C++ Reference">


> 每次我们使用变量名来输出对应的数据。
>
> 但是我们也能够通过它的地址来获取相应的内存地址，这个地址一般情况下每次都会变化（也可能不会）。在 C++ 里这个地址一般是以十六进制存储，至于 Python 则取决于它所在的平台，有时可能是个十六进制数，有时则有可能是其他的内容。

> 在 Python 里我们使用 `id` 函数，在 C++ 里则是运算符 `&`。
```cpp
#include <iostream>
using namespace std;

int main(){
    int varN = 101;
    cout << varN  << endl;  // 101
    cout << &varN << endl;  // 类似 0x7ffc9af603b4 这样的十六进制数 (id in Python)
    return 0;
}
```

> Python 和 C++都将变量存在内存中。其在内存中的位置可能会在每次运行时变化（也可能不会）。
>
> 根据上面的图例，我们看到 Python 并不能直接地存储变量：实际数据加上一个指向数据的引用。在 C++ 里变量可以直接存储相应的值。
>
> 引用这个过程很“慢”，但是有时它也非常有用。如果我们需要创建一个指向内存地址的引用，我们就需要使用一个挺特别的类型 —— 指针。


#### 2.5.1. 指针的语法
> 声明指针变量时原先的规则仍然适用，唯一你需要做的就是在类型与变量名之间加上 `*`。
```cpp
variableType *identifier;   // syntax to declare a C++ pointer
int          *ptrx;         // example of a C++ pointer to an integer
```

> 在 C++ 中空格在绝大多数情况下会被忽略，故以下写法作用完全相同
```cpp
SOMETYPE *variablename;     // preferable
SOMETYPE * variablename;
SOMETYPE* variablename;
```

> 第一种写法更优，我们一眼就能看出它是指针变量。

##### 2.5.1.1. ‘.. 的地址’运算符 `&`
> 现在我们知道了如何声明指针变量，可我们该如何把变量的地址赋给它呢？我们可以使用 `&` 运算符，我们只要把它放在变量名前就可以得到相应的内存地址。

> 以下是相应的赋值语法（`varN` 用于储存变量值，`ptrN` 存储变量 `varN` 在内存中的地址）：
```cpp
variableType *ptrN = &varN;     // 一个指针变量，其指向变量 varN 的地址
```

> 需要注意的是，指针变量的类型应与所指变量的类型相同

> 以下是扩展后的例子
```cpp
int varN = 9;
int *ptrN;      // 声明用于存储内存地址
ptrN = &varN;   // 存储内存地址
```

> 运行以上代码后
    >> <img src="../_images/chap02_sec05_pointer_decl_and_assign.png" height="auto" width="50%" margin="auto" alt="View into memory with pointers">


#### 2.5.2. 从指针访问变量值
> 你可以通过在指针变量前加上 `*` 来*解引用* <small>(dereference)</small>。即 `varN` 和 `*ptrN` 所指的是同一个值。

> 让我们再扩展下以上的例子来看看相关的变量值和它在内存中的地址：
```cpp
#include <iostream>
using namespace std;

int main() {
    int varN = 9;
    int *ptrN = &varN;

    cout << "varN value: "        << varN   << endl; // 9
    cout << "varN location: "     << ptrN   << endl; // 0xXXXXXXX
    cout << "dereference ptrN: "  << *ptrN  << endl; // 9

    return 0;
}
```

> 如果你将 `varN = 50;` 和 `cout << *ptrN << endl;` 放在指针变量 `ptrN` 的声明后，它会输出什么？（单选）
    >> a. `varPntr: 9`
    >> b. `varPntr: 50`
    >> c. `varPntr: 150`
    >> d. `0x7ffeb9ce053c`
    >> c. 以上都不是

> 以上代码编译运行后会输出：变量 `varN` 的值、指针变量 `ptrN` 里的东西（即 `varN` 的地址）以及 `ptrN` 所指向内存位置中的存储的值。
>
> 第二行输出的是变量 `varN` 的地址，此项输出数值因人而异：

> 想想看，如果你在给指针赋值时没有加上 `&` 运算符会发生什么？
```cpp
#include <iostream>
using namespace std;

int main( ) {
    int varN = 100;
    int *ptrN = varN; // Note no ampersand,
        // ptrN 现在指向内存中位置 100 处,
        // 我们现在完全不知道那里是否已被占用，
        // 所以你在运行时可能报错，也可能不会！

     cout << "varN value: "           << varN  << endl;
     cout << "ptrN location: "        << ptrN  << endl;
     cout << "ptrN points to varN: "  << endl;
     cout << "dereference ptrN: "     << *ptrN << endl;

     return 0;
}
```

> 糟了，糟了，糟了！
    >> <img src="../_images/chap02_sec05_pointer_dangling_reference.png" height="auto" width="50%" margin="auto" alt="C++ dangling pointer reference">

> 如果你的编译器并未捕捉到这个错误（尤其是这类），第一个 `cout` 将会输出 `After changing *ptrN, varN now has: 50`
>
> 第一行没有任何问题：你只是改变了被指向变量的值，指针所指的变量位置依旧未变。
>
> 第二行的 `cout` 问题大了：第一，你完全不知道内存位置 `100` 处上存储了什么东西；第二，位置 `100` 完全不在系统为当前程序分配的区域当中，操作系统可能会直接报 *存储器区段错误* <small>(segmentation fault)</small>。不过这个还算好的，这个错误信息直接给了你去哪里找的线索（比如指针），逻辑上的错误要隐蔽得多。


#### 2.5.3. 空指针
> 类似 Python 中的 `None`，C++ 语言中的 `nullptr` 也指向空值。老版本的 C++ 也是用 `NULL` 和数字 `0`。使用 `nullptr` 能够使编译器更容易作错误处理。在做逻辑判断中我们经常用空指针。
>
> 以下是空指针的例子。指针变量 `ptrx` 在进入循环前存储着变量 `x` 的地址，第一次循环过后，`ptrx` 被赋予 `nullptr`，此处循环停止因 `nullptr` 被解析为 `false`。

> 小技巧：空指针格外有用当你需要测试一个指针的状态，即指针所指位置是否合法。
```cpp
#include <iostream>
using namespace std;

int main( ) {
    int x = 12345;
    int *ptrx = &x;

    while (ptrx) {
        cout << "指针变量 ptrx 指向 " << &ptrx << endl;
        ptrx = nullptr;
    }

    cout << "指针变量 ptrx 不指向任何东西!\n";
}
```
