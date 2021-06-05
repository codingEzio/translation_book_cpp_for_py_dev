
### 3.2. `while` 循环
> 根据我们之前提到的，程序算法需要两个至关重要的控制结构：循环与选择。这两者都在  Python 中有相关的实现，开发者可以根据自己的情况选用。

> 针对需要重复的代码块，C++ 提供了 `while` 和 `for`。只要条件为真 `while` 循环会一直进行：
```cpp
int counter = 1;
while (counter <= 3) {
    cout << "Hello, world" << endl;
    counter = counter + 1;
}
```

> 以上将会输出五次 `"Hello, world"` 。`while` 的条件会在每次循环开始之前进行求值，若值得 `true` 代码块将会运行。

> 很多类算法都可能会用到 `while`。以下是使用复合条件的代码示例：
```cpp
while ( (counter <= 10) && (!done) ) {
    ...
}
```

> 因条件中 `&&` 运算符，以上的 `while` 循环只有在两个条件均为真时才会运行。

> 以下是其他的 `true-false` 布尔运算符：
```cpp
&&  // 和
||  // 或
!   // 相等
!=  // 不相等
>   // 大于
>=  // 大于或等于
<   // 小于
<=  // 小于或等于
```

> 另一个代码示例：
```cpp
#include <iostream>
using namespace std;

int main(){
    int counter = 0;
    while (counter <= 1) {
        cout << "Hello, world" << counter << endl;
    }
};
```

> 以下哪个是运行以上代码的结果？（单选）
    >> a. 不停地输出 `0`
    >> b. 输出一次 `"Hello, world"`
    >> c. 不停地输出 `"Hello, world"`
    >> d. 以上都不是