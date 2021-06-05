
### 3.3. `for` 循环
> 较于 `while`, `for` 循环能够更精准地控制循环的次数（`while` 只能在循环的代码块内加入新代码来实现同样的事情）：
```cpp
#include <iostream>
using namespace std;

int main() {
   for (int i = 0; i < 10; i++){
         cout << i << "hello world" << endl;
    }
 }
```

> 以上代码将会输出十次 `"hello world"`。另外 `for` 循环还适合于循环一定范围内的值：
```cpp
#include <iostream>
using namespace std;

int main() {
    for (int i=0; i<5; i++) {
        cout << i*i << " ";
    }

    return 0;
}
```

> 以上将会使用 `cout` 输出五次，输出分别是 `0`,`1`,`4`,`9`,`16`。
