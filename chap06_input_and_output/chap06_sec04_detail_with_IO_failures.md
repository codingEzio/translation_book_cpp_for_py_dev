
### 6.4. 应对未成功进行的输入输出操作 <small>(I/O Failures)</small>
> 文件的读写操作通常是运行时报错的高发区，故高质量的程序通常会包含有针对可能发生问题的错误处理。错误检查与处理一般需要开发者在函数中进行测试性的读写，以判断操作是否正常执行。在 C 语言里我们通过其返回值来判断，一般负值代表失败。在 C++ 里我们可以使用 `fail()` 成员方法判断其返回的布尔值。
```cpp
in_stream.fail();
```

> 这个函数只有在前一个文件流操作失败时才会返回 `true`，比如我们尝试去打开一个不存在的文件。如果真的发生了错误，我们应该立刻终止相关的读写操作以免避免更糟糕的后果。

> 以下代码块展示一旦读写有错误如何安全退出程序：
```cpp
#include <cstdlib>   // 使用其 exit 函数
#include <fstream>   // 使用其 文件流 定义
#include <iostream>  // 使用其 cout 函数
using namespace std;

int main() {
	ifstream in_stream;

    // 尝试打开文件 realFile.txt (用于读取)
	in_stream.open("myFile.txt");

	if (in_stream.fail()) {
		cout << "Sorry, the file couldn't be opened!\n";

        // 返回 1 代表当前程序有错误发生 (正常情况下一般为 0)
		exit(1);
	}

    return 0;
}
```

> 在打开 `myFile.txt` 文件后，`if` 会尝试判断打开过程中是否发生错误，若有即输出警告并退出程序。引自 `<cstdlib>` 的 `exit()` 方法用于在指定位置返回设定的数值并退出程序。
>
> 我们会在随后的章节中更深入地探讨错误处理。

