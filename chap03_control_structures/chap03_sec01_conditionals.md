
### 3.1. 条件式

> Python 的条件表达式和 C++ 的非常相似。

### 3.1.1. `if`
> 这个是 Python 的写法：
```python
if condition:
    statement1
    statement2
    ...
```

> 这个是 C++ 的写法：
```cpp
if (condition)  {
    statement1
    statement2
    ...
}
```

> 再强调一次：C++ 里使用花括号 `{}` 来分隔代码块而非缩进。`if` 在这里相当于是个函数（只会返回 `true` 或 `false`），故我们需要在条件两边加上括号。

### 3.1.2. `if else`
> 这个是 Python 的写法：
```python
if condition:
    statement1
    statement2
    ...
else:
    statement1
    statement2
    ...
```

> 这个是 C++ 的写法：
```cpp
if (condition) {
    statement1
    statement2
    ...
}
else {
    statement1
    statement2
    ...
}
```

### 3.1.3. `elif`
> 这个是 Python 的写法：
```python
def main():
    grade = 85

    if (grade < 60):    print('F')
    elif (grade < 70):  print('D')
    elif grade < 80:    print('C')
    elif grade < 90:    print('B')
    else:               print('A')

main()
```

> C++ 里没有对应的句式，但是我们可以通过嵌套 `if else` 来达到同样的效果：
```cpp
#include <iostream>
using namespace std;

int main() {
    int grade = 85;

    if (grade < 60)             { cout << 'F' << endl; }
    else {
        if (grade < 70)         { cout << 'D' << endl; }
        else {
            if (grade < 80)     { cout << 'C' << endl; }
            else {
                if (grade < 90) { cout << 'B' << endl; }
                else            { cout << 'A' << endl; }
            }
        }
    }
    return 0;
}
```

### 3.1.3.1. 考考你自己
> `if` 语句后一定要跟着一个 `else` 语句吗？
>
> 1. True
> 2. False

### 3.1.4. `switch`
> C++ 也支持有时运作起来类似 Python `elif` 的 `switch` 语句：它使用不同的 `case` 来判断是否执行特定代码块，这里的 `case` 为整数或是枚举常量值 <small>(*enum*erated constant)</small>。

> 以下是示例代码
```cpp
#include <iostream>
using namespace std;

int main() {
    int grade = 85;
    int tempgrade = grade / 10;

    switch(tempgrade) {
        case 10:
        case 9:
            cout << "The grade is A" << endl;
            break;
        case 8:
            cout << "The grade is B" << endl;
            break;
        case 7:
            cout << "The grade is C" << endl;
            break;
        case 6:
            cout << "The grade is D" << endl;
            break;
        default:
            cout << "The grade is F" << endl;
    }

    return 0;
}
```

> 不过说实话，`switch` 语句并不是那么常用。它比 `else if` 弱得多，因为它只能以整数或是枚举常量来判断是否相等；`break` 语句也特别容易被遗漏以导致副作用（假设你的 `grade` 是 `95`，当你把 `case 9` 后的 `break` 去掉后，程序会输出两个值分别是 `A` 和 `B`），所以平常还是避免使用 `switch` 语句吧！

### 3.1.4.1. 考考你自己

> 以下哪个符号用于包裹 `if` 的条件？（单选）
>
> 1. `{}`
> 2. `[]`
> 3. `()`
> 4. 任何一组括号都可以
> 5. 以上都不是
>
> `switch` 语句里如何避免所有的 `case` 都通过？（单选）
>
> 1. 以 `;` 结尾
> 2. 使用 `break` 语句
> 3. 以 `{}` 包裹每一个 `case`
> 4. 设置一个默认的 `case`
>
> C++ 里哪一个符号起到条件判断中 “和” 的作用？（单选）
>
> 1. 以 `;` 结尾
> 2. 使用 `break` 语句
> 3. 以 `{}` 包裹每一个 `case`
> 4. 设置一个默认的 `case`

