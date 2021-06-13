
### 5.6. 无序集合 <small>(Unordered Sets)</small>
> 无序集合由零个或多个无重复数据元素组成，所有元素类型均一致。你可以通过 `#include <unordered_set>` 来使用它：
>
> `unordered_set` 能够非常快速地根据给定的值取出特定元素。无序集合里元素的键与值是一样，每个元素都是独一无二的。无序集合里的键是不可改变的，但其可以被删除或插入他处。

> 无序集合的特点：元素不重复，不同元素之间用逗号 `,` 隔开：
```cpp
set<int> mySet = {3, 6, 4, 78, 10};
```

> 如果你有接触过数学里的集合的话，这些方法你应该会很熟悉：
>
| 方法名         | 使用方式             | 解释                                 |
| :------------- | :------------------- | :----------------------------------- |
| `union`        | `set_union()`        | 返回一个新集合包含两集合的所有元素   |
| `intersection` | `set_intersection()` | 返回一个新集合仅包含两者都有的元素   |
| `difference`   | `set_difference()`   | 返回一个新集合包含仅在前者中有的元素 |
| `add`          | `aset.insert(item)`  | 添加新元素至集合                     |
| `remove`       | `aset.erase(item)`   | 删除指定的元素                       |
| `end`          | `aset.clear()`       | 删去集合中的所有元素                 |

> 以下函数 `checker` 中的 `find` 方法用于判断是否有找到特定字符。其中 `set.find(letter) == set.end()` 是这样运作的：若 `find` 找到指定字符，它就返回指定字符（此等式即为 `false`）；若未找到则返回 `last`，其与 `set.end()` 相等，此等式也就为 `true`，即要寻找的字符并不在当前的无序列表中。
```cpp
// 此程序判断特定字符是否在指定的无序集合中
#include <iostream>
#include <unordered_set>
using namespace std;

void checker(unordered_set<char> set, char letter) {
    if (set.find(letter) == set.end()) {
        cout << "letter " << letter << " is not in the set." << endl;
    } else {
        cout << "letter " << letter << " is in the set." << endl;
    }
}

int main() {
    unordered_set<char> charSet = {'d', 'c', 'b', 'a'};

    char letter = 'e';
    checker(charSet, letter);

    charSet.insert('e');
    checker(charSet, letter);

    return 0;
}
```

#### 5.6.1. _
> 搭配部分已忽略
