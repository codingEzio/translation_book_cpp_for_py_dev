
### 6.11. 考考你自己
> 以下哪些库是用于输入输出的？（多选）
    >> a. `fstream`
    >> b. `ifstream`
    >> c. `ofstream`
    >> d. `iostream`

> 根据需求选择正确的库名：
>
| 库名       | 需求               |
| :--------- | :----------------- |
| `iostream` | 我想往终端写内容   |
| `fsstream` | 我想往文件中写内容 |

> 请问以下程序的输出是什么？（填空）
```cpp
#include <fstream>
#include <cstdlib>
#include <iostream>
using namespace std;

main(){
    ifstream in_stream;
    ofstream out_stream;

    int inputN;

    out_stream.open("anotherFile.txt");
    out_stream << 25;
    out_stream << 15 << endl;
    out_stream << 101 << endl;

    in_stream.open("anotherFile.txt");
    in_stream >> inputN;
    cout << inputN;
    in_stream >> inputN;
}
```
