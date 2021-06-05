
### 2.2. 布尔型数据
> 布尔数据类型是以英国数学家乔治・布尔 <small>(George Boole)</small>命名的，故此处 *Boolean*  首字母是大写。C++ 里的布尔类型通过 `bool` 声明，可选值只有两个：`true` 和 `false`，在 Python 里它们分别是 `True` 和 `False`。

> C++ 使用的是标准布尔运算符，与 Python 的对比：`&&` 与 `and` 、`||` 与 `or` 以及 `!` 与 `not`。另外，布尔值在内部实际上是以整数 `0`、`1` 存储的。
```cpp
#include <iostream>
using namespace std;

int main() {
    cout << true << endl;
    cout << false << endl;
    cout << (true || false) << endl;
    cout << (true && false) << endl;
    return 0;
}
```

> 布尔数据类型也可以被用在比较运算符中，比如 `==`、`>`。
| 运算名词  | 运算符  | 详解  |
|:-:|---|---|
| 小于 | `<` | 小于号 |
| 大于 | `>` | 大于号 |
| 小于等于 | `<=` | 小于等于号 |
| 大于等于 | `>=` | 大于等于号 |
| 相等 | `==` | 等号 |
| 不相等 | `!=` | 不等号 |
| 逻辑和 | `&&` | 两边运算对象均为真，结果为真（`true`）|
| 逻辑或 | `||` | 只要有一个运算对象为真，结果为真（`true`）|
| 逻辑非 | `!` | 将 `true` 变 `false`，将 `false` 变 `true` |

```cpp
#include <iostream>
using namespace std;

int main(){
    cout << (5 == 10) << endl;
    cout << (10 > 5) << endl;
    cout << ((5 >= 1) && (5 <= 10)) << endl;

    return 0;
}

```

> 当我们在声明变量后，相应的内存将会专门存储制定类型的数据。我们可以将类型声明和赋值合在一行内进行：
```cpp
#include <iostream>
using namespace std;

int main(){

    int theSum = 4;
    cout << theSum << endl;

    theSum = theSum + 1;
    cout << theSum << endl;

    bool theBool = true;
    cout << theBool << endl;

    theBool = 4;
    cout << theBool << endl;

    return 0;
}
```

> 以上 `int theSum = 0;` 创建了一个整型变量 `theSum` 并初始化它为 `0`。在 Python 里，等号右边的赋值会先被“解释”，其产生的数据会被赋值给相应的变量。因为 Python 是动态类型，故一旦等号右边的值的类型发生变化，相应变量的类型也会变化。在 C++ 里这完全不存在，一个类型只能存一种类型的数据。现在来考考你是否理解了这一段：

> 为什么 `theBool` 的输出仍为 `1` 即使已经被设置为 `4` 了？（单选）
    >> a. 将 `theBool` 设置为任何非 `true`、`false` 的值 都会被忽略
    >> b. 将 `theBool` 设置为任何大于 `0` 的值都为 `true`，否则为 `false`
    >> c. 因 `false == 0`、`true != false`，故任何非 `0` 的值转换为布尔类型均为 `true`
    >> d. 以上都不是
