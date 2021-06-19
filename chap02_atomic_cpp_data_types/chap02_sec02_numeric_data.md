
### 2.2. 数字型数据
> 数字型数据类型包含有 `int`、`float` 以及 `double`。
>
> 你可以通过对 `+ - * /` 加入括号来选择哪些优先级更高。
>
> 在 Python 里我们使用 `//` 来得到整数相除（即 `4 // 3 == 1`）。在 C++ 我们只使用 `/`，但是有两种情况：两个整数相除后，其效果和 Python 里一样（整除）；但如果其中一个数为浮点数，其结果将也会是浮点数，并且整除的规则不再适用。
>
> 在 C++ 里我们使用 `cmath` 库里的 `pow()` 进行指数计算，取商和 Python 一致（使用 `%`。

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main(){
    cout << (2+3*4) << endl;        // 2+3*4    (Python)
    cout << (2+3)*4 << endl;        // (2+3)*4  (Python)
    cout << pow(2, 10) << endl;     // 2**10    (Python)
    cout << float(6)/3 << endl;     // 6/3      (Python)
    cout << float(7)/3 << endl;     // 7/3      (Python)
    cout << 7/3 << endl;            // 7//3     (Python)
    cout << 7%3 << endl;            // 7%3      (Python)
    cout << float(3)/6 << endl;     // 3/6      (Python)
    cout << 3/6 << endl;            // 3//6     (Python)
    cout << 3%6 << endl;            // 3%6      (Python)
    cout << pow(2, 100) << endl;    // 2**100   (Python)
    return 0;
}
```

> 当声明数字型数据时，我们还可以在类型前加上 `short`、`long`、`unsigned` 这样的前缀，以确保每个数据都得到了适合自己的内存空间大小。

> 哪一个是 `3/2` 的结果（C++）？（多选 ）
>
> 1. `1`
> 2. `1.5`
> 3. `2`
> 4. 运行错误
> 5. 以上都不是
>
> 在 C++ 里如何如何计算 4 的 5 次幂？（多选 ）
>
> 1. `4**5`
> 2. `5**4`
> 3. `4^5`
> 4. `pow(4,5)`
