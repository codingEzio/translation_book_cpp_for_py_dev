
### 5.5. 哈希表 <small>(Hash Tables)</small>
> 如果你有用过 Python 中字典 <small>(`dict`)</small> 的话，那么你就已经使用过了 *哈希表*。哈希表是由一系列相联的键值对组成的集合，它们通常又被称为 *映射* <small>(map)</small>。当然了，哈希表是更推崇的正式名称，为什么？因为并不是所有的映射都是由哈希表实现的。
>
> 每个哈希表都会有一个哈希函数，其用于接收字典键并返回其对应值的内存地址，这种方式使得查找的速度非常快。

> 字典类型在 Python 里开盒即用，C++ 你则需要另外导入相关的库来使用：
```cpp
#include <unordered_map>
```

> C++ 里哈希表的语法与 Python 的字典相差无几。相较于数组使用索引来访问元素，哈希表使用键。Python 与 C++ 的哈希表都可以预先初始化，也可以随后添加新数据。在 C++ 里，大括号里第一个关键词为键，第二个为值。
```cpp
// 数字一到四的对应表（左侧：英语，右侧：西班牙语）
#include <iostream>
#include <unordered_map>
#include <string>
using namespace std;

int main() {
    unordered_map<string, string> spnumbers;
    spnumbers = { { "one" : "uno" },
                  { "two" : "dos" }  };

    spnumbers["three"] = "tres";
    spnumbers["four"]  = "cuatro";

    cout << "one is ";
    cout << spnumbers["one"] << endl;

    cout << spnumbers.size() << endl;
}
```
```python
# 此实现与以上 C++ 版本的功能相同
def main():
    spnumbers = { "one" : "uno" ,
                  "two" : "dos"  }

    spnumbers["four"]  = "cuatro"
    spnumbers["three"] = "tres"

    print("one is", end=" ")
    print(spnumbers["one"])

    print(len(spnumbers))

main()
```

> 值得注意的是，哈希表是由其函数给出的位置整理的，而不是按照任何特定的顺序，这使其查找速度非常非常快（甚至优于数组）。虽然在 C++ 与 Python 你都能够利用其特性来遍历它，但因它并非是有序存储的故这种操作并不常见。`unordered_map` 的迭代器通过指针来指向特定元素的键值：
```cpp
// 数字一到五的对应表（左侧：英语，右侧：西班牙语）
#include <iostream>
#include <unordered_map>
#include <string>
using namespace std;

int main() {
    unordered_map<string, string> spnumbers;
    spnumbers = { { "one"   : "uno"    },
                  { "two"   : "dos"    },
                  { "three" : "tres"   },
                  { "four"  : "cuatro" },
                  { "five"  : "cinco"  }  };

    // auto 关键字能够自己推断出正确的变量类型
    for (auto i = spnumbers.begin(); i != spnumbers.end(); i++ ){
        cout << i->first << ":";
        cout << i->second << endl;
    }
}
```
```python
# 此实现与以上 C++ 版本的功能相同
def main():
    spnumbers = { "one"   : "uno"   ,
                  "two"   : "dos"   ,
                  "three" : "tres"  ,
                  "four"  : "cuatro",
                  "five"  : "cinco"   }

    for key in spnumbers:
        print(key, end=":")
        print(spnumbers[key])

main()
```

> 以下是哈希表的运算符以及一些常用的方法：
>
| 运算符  | 使用方式           | 解释                                        |
| :------ | :----------------- | :------------------------------------------ |
| `[]`    | `mymap[key]`       | 返回键 `key` 的值，若无即报错               |
| `count` | `mymap.count(key)` | 哈希表里有此键返回 `true`，若无返回 `false` |
| `erase` | `mymap.erase(key)` | 删除指定的键及相关的值                      |
| `begin` | `mymap.begin()`    | 返回一个指向指向首个元素的迭代器            |
| `end`   | `mymap.end(key)`   | 返回一个指向越过尾部元素的迭代器            |

https://runestone.academy/runestone/books/published/cpp4python/CollectionData/HashTables.html#matching
#### 5.5.1. 搭配
| 操作函数 | 解释 |
| :------- | :--- |
| `_`      | _    |
| `_`      | _    |
| `_`      | _    |
| `_`      | _    |
| `_`      | _    |
