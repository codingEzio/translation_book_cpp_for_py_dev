
### 5.3. 向量
> 向量 <small>(vector)</small> 实际上要比数组更像 Python 里的 list。向量通过动态分配的数组存储元素，不同于数组，它们即使在声明后仍然可以改变大小，以及其他有用的功能。它们存储数据的方式仍允许用户能够按着顺序访问和遍历元素，另外，如果你只是想访问特定元素也是可以的。向量的大小是动态的，所以当有新元素被添加或是元素被删去时，向量的大小都会重新被分配。与 Python 不同的一点是，向量中所有的元素只能是同一个类型的。

> 若要使用向量，你可以通过导入标准模板库 <small>(*S*tandard *T*emplate *L*ibrary)</small> 来使用：
```cpp
#include <vector>
```

> 一些常用的方法
>
| 向量操作    | 使用方式                 | 解释                       |
| :---------- | :----------------------- | :------------------------- |
| `[]`        | `myvect[i]`              | 访问在索引 `i` 处的元素    |
| `=`         | `myvect[i] = value`      | 赋值给在索引 `i` 处的元素  |
| `push_back` | `myvect.push_back(item)` | 添加元素至向量末尾处       |
| `pop_back`  | `myvect.pop_back()`      | 删除向量末尾处的元素       |
| `insert`    | `myvect.insert(i, item)` | 在索引 `i` 处插入新元素    |
| `erase`     | `myvect.erase(i)`        | 删除在索引 `i` 处的元素    |
| `size`      | `myvect.size()`          | 返回元素数量               |
| `capacity`  | `myvect.capacity()`      | 返回向量实际能够容纳的空间 |
| `reserve`   | `myvect.reserve(amount)` | 改变容纳空间               |

> 我们通常会使用 `push_back()` 方法来增加向量的大小。因为其能在声明后改变大小的特性，向量通常会额外分配一些空间以预备未来可能的扩张。这也是为什么向量的容纳空间往往要比其元素数量多。


#### 5.3.1. 遍历向量
> 要遍历向量的元素你只需要调用 `.length()` 函数即可；至于数组，你需要先用 `sizeof()` 函数得到其元素数量，然后通过 `sizeof()` 得到单个元素的大小（之所以可以这样做是因为其所有的元素类型相同）两者相除即可。

> 第二个 for 循环暂被注释掉了，这是为了兼容性的原因。老版如 C++03 之前的版本均不支持这种语法，[在 C++ 11 该方式被引入](https://en.cppreference.com/w/cpp/language/range-for)。
```cpp
#include <iostream>
using namespace std;

int main() {
    int nums[]   = { 1, 3, 6, 2, 5 };
    int numsSize = sizeof(nums) / sizeof(nums[0]);

    // index loop
    for (int index = 0; index < numsSize; index++) {
        cout << nums[index] << endl;
    }

    cout << endl;

    // iterator loop
    for (int item:nums) {
        cout << item << endl;
    }

    return 0;
}
```

> 每次循环 `index` 的值都向 `numsSize` 递增，故每次你都能得到相应索引处的值。

https://runestone.academy/runestone/books/published/cpp4python/CollectionData/Vectors.html#matching
#### 5.3.1.1 搭配
| 操作函数 | 解释 |
| :------- | :--- |
| `_`      | _    |
| `_`      | _    |
| `_`      | _    |
| `_`      | _    |
| `_`      | _    |
| `_`      | _    |
| `_`      | _    |
| `_`      | _    |
| `_`      | _    |

> 以下 C++ 例子中的 `reserve` 方法完全是可选的。但是为了节省(内存重新分配的)时间，我们一般会在向量变大之前就提前预留出空间。更详细的解释：因为向量是存在连续的内存块上，每次当其元素数量超过可容纳空间时，整个向量都需要被复制到更大的内存空间处，这些复制都需要花费时间。通常的实现是：一旦元素数量过大，其可容纳空间会扩充为原先的两倍。
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main(){
    vector<int> intvector;
    intvector.reserve(50);

    for (int i = 0; i < 50; i++){
        intvector.push_back(i * i);
        cout << intvector[i] << endl;
    }
    return 0;
}
```
```python
def main():
    intlist = []

    for i in range(50):
        intlist.append(i * i)

        print(intlist[i])

main()
```

> 以下是容器自动扩充两倍的示例代码：
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main(){

    vector<int> intvector;
    // 不使用 intvector.reserve(50);

    for (int i = 0; i < 50; i++){
        intvector.push_back(i * i);
        cout << intvector[i] << endl;
        cout << "capacity: " << intvector.capacity() << endl;
    }
    return 0;
}
```

> 时刻记住：在 C++ 中速度为王，越界保护完全是次要考虑：
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main(){
    vector<int> intvector;
    intvector.reserve(10);

    for (int i = 0; i < 10; i++){
        intvector.push_back(i);
    }

    for (int i = 0; i <= 10; i++){
        cout << "intvector[" << i << "]=" << intvector[i] << endl;
    }

    return 0;
}
```
```python
def main():
    intlist=[]
    for i in range(10):
        intlist.append(i)

    for i in range(11):
        print(f"intlist[{str(i)}]={str(intlist[i])}")

main()
```

> C++ 中数组和向量最大的区别是什么？（单选）
    >> a. 向量可以在声明后改变大小
    >> b. 向量能够提供类似 Python 里 list 的所有功能和越界保护
    >> c. 向量并不存在连续的内存块上，所以元素可以自由被插入
    >> d. 有多个答案
    >> e. 以上都不是
>
> 使用向量的 `reserve` 方法有什么好处？（单选）
    >> a. 没什么额外的好处。完全是可选使用的。
    >> b. 如果你预先能够知道元素的总数量，使用它能够节省(内存重新分配的)时间
    >> c. 给向量分配内存只能通过这个方法
    >> d. 以上都不是
