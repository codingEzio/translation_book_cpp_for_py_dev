
### 5.4. 字符串
> 字符串是一个由零个或多个字符组成的序列集合。在 C++ 里有两种字符串类型：头一种是相对比较近代的 C++ string （通过导入 `<string>` 使用），它与 Python 中的字符串类型很相似；另一种是相对老一些的 C-string，它本质上是由单个字符组成的字符数组。字符类型与以上提到的字符串完全不是一回事。
```cpp
char   cpp_char = 'a';                  // 字符类型使用单括号
string cpp_string  = "Hello World!";    // C++ string 使用双括号
char   cpp_cstring = {"Hello World!"};  // C-string (或字符数组)使用双括号
```

> 在老版 C++ 里你必须使用 `char` 数组来构建用户名。在 C++ 11 后较现代的版本里，你可以用 C++ string 做任何事。鉴于 C++ string 与 Python 中的字符串很相似，我非常不建议你使用老旧的 C-string。

> 选出 c-stings 的正确定义。（单选）
    >> a. 存储在数组内的一系列字符，由 `\0` 结尾
    >> b. 一个连续性的数据结构，由零个或多个元素组成
    >> c. 一个有序的集合数据元素，可通过索引访问特定元素
    >> d. 一个存储单个类型数据的序列容器，其底层是能够改变大小的动态数组

> 因为字符串也是序列，故之前你学到的数组操作在这里多数可以照搬。这里新增的还有一些常用的字符串方法：
>
| 方法名      | 使用方式                    | 解释                           |
| :---------- | :-------------------------- | :----------------------------- |
| `[]`        | `astring[i]`                | 访问在索引 `i` 处的字符        |
| `=`         | `astring[i] = value`        | 修改在索引 `i` 处的字符        |
| `+`         | `astring + astring2`        | 连接字符串                     |
| `append`    | `astring.append(string)`    | 添加新字符串至字符串末尾       |
| `push_back` | `astring.push_back(char)`   | 添加新字符至字符串末尾         |
| `pop_back`  | `astring.pop_back()`        | 删除字符串末尾处的单个字符     |
| `insert`    | `astring.insert(i, string)` | 在索引 `i` 处插入新字符串      |
| `erase`     | `astring.erase(i, j)`       | 删除自索引 `i` 至 `j` 处的元素 |
| `find`      | `astring.find(item)`        | 返回首次找到指定字符的索引位置 |
| `size`      | `astring.size()`            | 返回字符串大小                 |


#### 5.4.1. _
> 搭配部分已忽略

```cpp
#include <iostream>
#include <string>
using namespace std;

// 返回字符串 "World!" 在拼接后字符串的起始索引
int main(){
    string mystring1 = "Hello";
    string mystring2 = "World!";
    string mystring3;

    mystring3 = mystring1 + " " + mystring2;
    cout << mystring3 << endl;

    cout << mystring2 << " begins at ";
    cout << mystring3.find(mystring2) << endl;

    return 0;
}
```
```python
# 此实现与以上 C++ 版本的功能相同
def main():
    mystring1 = "Hello"
    mystring2 = "World!"

    mystring3 = mystring1 + " " + mystring2
    print(mystring3)

    print(mystring2, end=" ")
    print("begins at", end=" ")
    print(str(mystring3.find(mystring2)))

main()
```

> 选出每个初始方式对应的语法
>
| 类型       | 语法    |
| :--------- | :------ |
| string     | `'a'`   |
| char       | `"a"`   |
| char array | `{'a'}` |