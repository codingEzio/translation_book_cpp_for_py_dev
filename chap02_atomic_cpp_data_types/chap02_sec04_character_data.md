
### 2.2. 字符型数据
> Python 里你可以使用单括号或双括号来创建字符串。在 C++ 里前者用于字符 <small>(`char`)</small> 数据类型，后者用于字符串 <small>(`string`)</small> 类型。
```cpp
#include <iostream>
#include <string>
using namespace std;

int main(){
    string strvar = "b";
    char charvar = 'b';

    cout << ('b' == charvar) << endl;
    cout << ("b" == strvar) << endl;
    cout << ('a' != "a") << endl;       // 不同类型无法直接比较，故会报错

    return 0;
}
```

> 如果我想创建一个字符串，我该使用那个符号？（单选）
    >> a. `''`
    >> b. `""`
    >> c. `''` 或 `""` 都可以
    >> d. 取决于语言实现
    >> e. 以上都不是
