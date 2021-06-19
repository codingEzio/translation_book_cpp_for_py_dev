
### 6.6. 文件末尾 <small>(EOF)</small>
> 直到目前我们都假设开发者知道要读从打开的文件中读多少内容，实际情况则不然。几乎所有的 C++ 版本都实现有 *文件末尾* <small>(EOF)</small> 的标志，我们在读文件时即可以利用它来判断何时停止读的操作。如果没有实现此标志，我们可能打开了 *X* 文件，但实际上我们是在读其他文件，这带来的副作用可能是灾难性的。
>
> 多数开发环境都有定义 `eof()` 成员方法，以判断文件末尾标志的值是 `true` 还是 `false`。我们在读文件时需要随时判断是否已经到达了文件末尾（若未到则继续读取），故我们通过会用其返回值求负来判断。另外一种解决方案则是用 `>>` 运算符不断读取：如果其操作成功执行（有读到内容，非空），其返回值便会被解析为能用作判断的布尔值（如 `1` 转换为 `false`）。
>
> 以下代码展示了两种读取的方案：

> 使用 `eof()` 成员方法：
```cpp
while ( !in_stream.eof() ) {
    // 只要未达到文件末尾 (EOF) 就继续执行
}
```

> 使用 `>>` 运算符：
```cpp
while ( in_stream >> inputN ) {
    // 至少上一次的读取中包含内容 就继续执行
}
```

> 以下程序利用的是第二种方式（子函数 `make_neat()` 里的 `while` 循环）：读入一个文件内的所有数字，然后将其格式整理后输出到另外一个文件（以及终端）。
```cpp
// 以下程序主要展示了如何在输出前调整格式 (通过不同的指令).
// 读入 rawdata.dat 中的所有数字, 然后将其格式美化后输出至终端以及 neat.dat 文件.

#include <cstdlib>   // 使用其 exit 函数
#include <fstream>   // 使用其 文件流 定义
#include <iomanip>   // 使用其 setw 函数
#include <iostream>  // 使用其 cout 函数
using namespace std;
void make_neat(ifstream &messy_file, ofstream &neat_file,
               int number_after_decimalpoint, int field_width);

int main() {
    ifstream fin;
    ofstream fout;

    fin.open("rawdata.txt");
    if (fin.fail()) {  // 用于读取的文件不存在?
        cout << "Input file opening failed." << endl;
        exit(1);
    }

    fout.open("neat.dat");
    if (fout.fail()) {  // 无法打开输出文件!
        cout << "Output file opening failed.\n";
        exit(1);
    }

    make_neat(fin, fout, 5, 12);

    fin.close();
    fout.close();
    cout << "End of program." << endl;

    return 0;
}

// 使用 iostreams (输出至终端) 和 iomanip (调整输出格式).
void make_neat(ifstream &messy_file, ofstream &neat_file,
               int number_after_decimalpoint, int field_width) {
    // 为输出文件调整格式
    neat_file.setf(ios::fixed);
    neat_file.setf(ios::showpoint);
    neat_file.setf(ios::showpos);
    neat_file.precision(number_after_decimalpoint);

    // 为终端输出调整格式
    cout.setf(ios::fixed);
    cout.setf(ios::showpoint);
    cout.setf(ios::showpos);
    cout.precision(number_after_decimalpoint);

    double next;
    while (messy_file >> next) {  // 只要还能读到内容, 就继续执行 while 循环
        cout      << setw(field_width) << next << endl;
        neat_file << setw(field_width) << next << endl;
    }
}

// 该代码由 Jan Pearce 编写
```

> 这些数据将被以上的函数读取（故你需要将这些数据先保存为 `rawdata.txt` 文件）：
```cpp
// 输入文件 rawdata.txt
10 -20 30 -40
500 300 -100 1000
-20 2 1 2
10 -20 30 -40
```

> 以下是我们期望看到的程序输出（输出文件名为 `neat.dat`）：
```cpp
  +10.00000
  -20.00000
  +30.00000
  -40.00000
 +500.00000
 +300.00000
 -100.00000
+1000.00000
  -20.00000
   +2.00000
   +1.00000
   +2.00000
  +10.00000
  -20.00000
  +30.00000
  -40.00000
```

> 在执行程序时，你要确保你的代码和含有数据的 `rawdata.txt` 在同一目录。若程序成功执行，它会创建一个名为 `neat.dat` 的文件。

> 选出 C++ 里的 EOF 的使用场合。（多选）
>
> 1. 保证程序不会往不相关的文件写数据
> 2. 保证程序不会终止
> 3. 保证你的程序不会溢出到缓冲区里
> 4. 终止输入文件流
