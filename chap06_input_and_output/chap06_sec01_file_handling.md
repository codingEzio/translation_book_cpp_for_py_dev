
### 6.1. 文件操作
> C++ 里的文件借用 `<iostream>` 里 *流* 的概念来操作。若要对文件进行读写需要导入 `<fstream>` 库。

> 在读写任何文件前你都必须预先声明相关的文件流。以下语句用于告知编译器创建相关的流：`ifstream` 用于读取文件，`ofstream` 则用于创建及往文件写内容。
```cpp
ifstream in_stream;
ofstream out_stream;
```
