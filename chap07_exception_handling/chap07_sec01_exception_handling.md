
### 7.1. 异常处理 <small>(Exception Handling)</small>
> 写程序时最常见的有两种错误：第一个是语法错误，说白了就是开发者在语句或表达式中未按正确的语法编写。以下就是一个很好的例子（在声明行的末尾未使用分号）：
```cpp
int main() {
    int i = 10
    return 0;
}

// 原作者的错误消息 (也可能是单纯为了演示)
>>  exit status 1
    main.cpp: In function 'int main()':
    main.cpp:3:5: error: expected ',' or ';' before 'return'
         return 0;
     ^~~~~~

// 译者的错误消息 (编译器以及版本: clang++ -std=c++14)
main.cpp:2:15: error: expected ';' at end of declaration
    int i = 10
              ^
              ;
1 error generated.
```

> 在上边的代码中，声明语句后没有遵循语法规则加上分号，所以第一步的编译就无法通过。你学习新语言时最常遇到的可能就是语法错误。
>
> 逻辑错误则不然：程序能够正常运行，但其给出的结果是错误的；有些情况下这可能是因为你使用的第三库中的代码有问题，又或者是你在把业务逻辑转换为实际代码的过程中出现了问题。有时这种错误会导致非常糟糕的后果，比如除以数字 `0` 或是一个数组访问超出自己边界的数值。这些假想的错误会进一步演变为 *运行时错误* <small>(runtime error)</small> 从而终止程序的运行，这类运行错误一般被称为 *异常* <small>(exceptions)</small>。
>
> 在遇到程序异常退出时，新手开发者可能觉得无从下手。实际上，多数编程语言都允许开发者对可能发生的异常进行处理。而且，开发者还可以根据业务逻辑创建自定义的异常。

> 当异常发生时，我们将其称为 "抛出(异常)"。你可以使用 `try` 来捕捉 <small>(`catch`)</small> 被 *抛出* 的异常。设想这样一个程序：从用户接收两个整数然后对两者进行除法操作；正常情况下，这个程序能够正常执行，并输出正确的结果；但是，一旦用户在第二个参数处输了数字 `0`，程序会立即报错并返回一个非 `0` 的值（代表有错误发生）。
```cpp
main.cpp: In function 'int main()':
main.cpp:5:13: warning: division by zero [-Wdiv-by-zero]
   cout << 10/0;
           ~~^~
exit status -1
```

> 我们可以通过创建一个 `div` 函数来捕捉这个错误，然后以我们自己的方式抛出。`try` 和 `catch` 合并起来不仅能够 *捕捉* <small>(catch)</small> 到异常，还能在异常发生的位置输出用户自定义的信息。让我们来看下这个示例程序：
```cpp
// 程序目的: 通过 try 代码块 和 throw+catch 两者协作(一个丢,一个捕) 来演示异常处理
#include <iostream>
using namespace std;

double div(double num1, double num2) {
    if (num2 == 0) {
        // 如果第二个数字为 0, 抛出这个错误
        throw "Cannot divide by 0!\n";
    }

    return num1 / num2;
}

int main() {
    // 从用户接收输入
    float firstNum=10;
    float secondNum=0;

    try {
        // 尝试对这两个数字进行除法操作
        double result = div(firstNum, secondNum);
        cout << "result of division: " << result << endl;

    }
    catch (const char *err) {
        // 如果有错误被抛出, 输出错误信息
        cout << err;
    }

    return 0;
}
```

> 以上程序能够通过 `div` 函数捕捉到预期的异常，并且输出异常信息。此程序最大的不同在于：当遇到异常时并不会终止，它能够继续执行到程序的末尾（假设之后没有异常情况的话）。
>
> 开发者还能够嵌套使用 `try .. catch` 来更精细地处理不同的异常。上述程序选择了 *捕捉并输出自定义错误信息* 的方式，我们也可以选择 *返回错误码* <small>(error code)</small> 然后终止程序。

> 以下代码应在一个含有 `file.txt` 文件的目录下运行，如果没有其实也没问题。此程序能够捕捉不同情形下的异常：不管是用户指定的文件不存在，还是默认的 `file.txt` 也不存在。
```cpp
// 以下程序能够用来打开文件.
#include <fstream>
#include <iostream>
using namespace std;

void printFile(char filename[32]) {
    ifstream in_stream;
    in_stream.open(filename);

    if (!in_stream.good()) {
        // Throws an error
        in_stream.close();

        throw "\nA file by that name does not exist!";
    }

    char ch;

    cout<<endl;
    while (!in_stream.eof()) {
        cout << ch;
        ch = in_stream.get();
    }
    cout << endl;

    in_stream.close();
}

int main() {
    char filename[32];
    cout << "Filename: ";
    cin >> filename;

    try {
        // 尝试输出文件内容
        printFile(filename);
    }
    catch (const char *msg) {
        // 如果上边的 printFile 抛出了异常, 此行将会运行
        cerr << msg << endl; // 类似 cout, cerr 只用于输出错误信息

        // 改用默认的文件名 (用于打开读取)
        try {
            char defaultFile[32] = "file.txt";
            printFile(defaultFile);
        }
        catch (const char *msg) {
            cerr << "Default file not found!" << endl; // 类似 cout, cerr 只用于输出错误信息
        }
    }

    return 0;
}
```

> C++ 标准库里还有许多用户可以选用的异常。请移步至官方文档查看所有可用的异常类型，以及如何创建你自己的异常类型。
