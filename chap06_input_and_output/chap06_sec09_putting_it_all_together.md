
### 6.9. 全面回顾
> 以下程序涵盖了所有我们之前提到过的概念。它是这样运作的：请求用户键入两个文件名，一个用于读，另一个用于写；检查是否正常打开了指定文件；从打开的文件读入三个数字，然后将其总和写入另一个文件中。
```cpp
#include <cstdlib>   // 使用其 exit 函数
#include <fstream>   // 使用其 文件流 定义
#include <iostream>  // 使用其 cout 函数
using namespace std;

int main() {
    char in_file_name[16],
        out_file_name[16];  // 规定文件名的最大长度为 15 个字符
    ifstream in_stream;
    ofstream out_stream;

    cout << "该程序将从用户指定的文件中读三个数字, 计算总和后把其写入另一个文件." << endl;

    cout << "请键入含三个数字的文件的名字 (至多 15 个字符):\n";
    cin  >> in_file_name;

    cout << "\n请键入用于写入三数字总和文件的名字 (至多 15 个字符):\n";
    cin  >> out_file_name;

    cout << endl;

    // 将两文件集中在一起打开，一同检测.
    in_stream.open(in_file_name);
    out_stream.open(out_file_name);

    if (in_stream.fail() || out_stream.fail()) {
        cout << "无法打开文件 (任一或两者).\n";
        exit(1);
    }

    double firstn, secondn, thirdn, sum = 0.0;

    cout << "自文件中读数字: " << in_file_name << endl;
    in_stream >> firstn >> secondn >> thirdn;

    sum = firstn + secondn + thirdn;

    // 以下两行将会输出至终端处
    cout << "来自 " << in_file_name << " 文件的总和为 "
         << sum << endl;
    cout << "将总和写入该文件: " << out_file_name << endl;

    // 以下一行的输出将会写入文件 (该行暂不翻译, 暂无精力解决可能出现的中文字符写入问题)
    out_stream << "The sum of the first 3 numbers from " << in_file_name << " is "
               << sum << endl;

    in_stream.close();
    out_stream.close();

    cout << "程序结束." << endl;

    return 0;
}
```
