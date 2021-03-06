
### 4.4. 函数重载
> 函数重载是多次实现一个函数，但每个接收的参数不同。并不是所有的语言都支持这样，比如 `Python` 就不支持。
>
> C++ 里的多个函数可以有同样的名字，以接收不同的函数参数来区分，其可以是不同的类型，也可以只是参数数量上的差别。

> 在 Python 里若想达到类似的结果，你则需要在函数内部进行逻辑判断。
```cpp
#include <iostream>
using namespace std;

void myfunct(int n) {
     cout << "1 parameter: " << n <<endl;
}

void myfunct(int n, int m) {
     cout << "2 parameters: " << n;
     cout << " and " << m <<endl;
}

int main() {
    myfunct(4);
    myfunct(5, 6);
    myfunct(100);

    return 0;
}
```

> 函数重载的优点有哪些？（多选）
>
> 1. 保证函数命名上的统一
> 2. 对于不同的需求以参数来区分，而不是函数名称
> 3. 函数可通过仅仅参数的差别就完成不同的任务
> 4. 对传入参数的数量不作任何限制

<hr/>

> ***自我测验***
>
> 你听说过无限猴子定理吗？其表述为：让一个猴子在打字机上随机性地按键，只要有足够长的时间它一定能够写出任何人类的优秀著作，比如莎士比亚的全套著作。现在，我们用一个 C++ 程序来代替之前提到的猴子，你觉得这个程序需要多久才能实现同样的需求呢？我们先定一个小目标，生成 `methinks it is like a weasel`。
>
> 由于这个程序要复杂的多，你最好是打开集成开发环境在实机上运行它。我们需要实现三个函数（小提示：库 `random` 在这里会很实用）：第一个用于生成长度为 28 的字符串（英文字母、空格以及字符串结尾）；第二个用于对比评估生成的字符串与所要求的目标字符串。
>
> 最后一个则是不断地重复前两个函数的操作，随机生成然后评估是否 100% 相似，一旦其达到 100% 即达到了我们的目标；若没有，那就继续重复生成评估这个过程。鉴于此程序会生成大量的输出，你可以让它每尝试一千次只输出其中近似度最高的结果。

> ***自我挑战***
>
> 你可以尝试下如何在已输入正确字母不变的情况下，只修改不正确的字母。这类算法又被称为 *爬山算法*，其只有在当次结果比上次更优的情况下才会保留相关输出。
