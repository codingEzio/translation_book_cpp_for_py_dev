
### 4.2. 参数参数・传值与传引用
> 至今我们写的函数都是使用传值的方式。调用这类函数时，传入的参数值会被拷贝到相应参数的内存位置。即使函数内对传入参数进行了修改操作，原先传入的函数变量也不会被影响。

> 代码示例
```cpp
void functionExample(int inputVar) {
    int nextVar = inputVar * 2;
    inputVar = 4;

    cout << "nextVar = " << nextVar << " inputVar = " << inputVar;
}

void callingFunction() {
    int myVar = 10;

    functionExample(myVar);
    cout << "myVar = " << myVar;
}
```

> 当函数 `callingFunction` 执行时，它调用函数 `functionExample(...)` 并将 `myvar` 作为参数传入。在 `functionExample(...)` 函数内，值 `10` 自 `myvar` 被复制进了 `functionExample(...)` 函数的参数 `inputvar`。以下是 `functionExample(...)` 函数的输出：`nextVar = 20  inputVar = 4`

> 我们可以注意到即使在调用 `functionExample(...)` 函数后 `myvar` 数值依旧未变，这是因为两者（myVar 和 inputVar）分别存储在内存上的不同位置。即使我们在 `functionExample(...)` 函数里修改了参数 `myVar`，主函数的输出依然是：`myVar = 10`。
>
> 简单地说，任何对变量的修改都是局部性即限于函数内部的。
> 我们现在看了很多传递一个参数或者什么都不传的函数，如果我们想要传递不止一个参数呢？这时我们就需要使用另一种传递方式：传引用。不同于传值，这种方式会将参数的内存地址直接传给函数。使用它也很简单，你只需要在函数参数前加上 `&` 即可。通过这种方式传值的函数能够直接修改传入参数。

> 让我们来看一个通过这种方式传递参数的函数：
```cpp
#include <iostream>
using namespace std;

void swap_values(int &variable1, int &variable2) {
    int temp;

    temp = variable1;
    variable1 = variable2;
    variable2 = temp;
}

int main( ) {
    int first_num, second_num;
    first_num = 7;
    second_num = 8;

    cout << "交换前: 1) " << first_num << " 2) " << second_num << endl;
    swap_values(first_num, second_num);
    cout << "交换后: 1) " << first_num << " 2) " << second_num;

    return 0;
}
```

> 我们若想通过外部函数修改传入的参数，我们必须使用传引用的方式来实现。你可以把 `&` 去掉看看会怎么样。

> 分析下这个程序并回答下边的两个问题：
```cpp
#include <iostream>
using namespace std;

void func1(int var1, int var2){
    int temp;
    temp = var1;
    var1 = var2;
    var2 = temp;
}

void func2(int &var1, int &var2){
    int temp;
    temp = var1;
    var1 = var2;
    var2 = temp;
}

int main(){
    int num1 = 2;
    int num2 = 3;

    func1(num1, num2);
    cout << "func1 结果: " << endl;
    cout << "num1: " << num1 << ", num2: " << num2 << endl;
    func2(num1, num2);
    cout << "func2 结果: " << endl;
    cout << "num1: " << num1 << ", num2: " << num2 << endl;

    return 0;
}
```

> 这两个函数的区别是什么 (`func1` 和 `func2`)？（多选）
>
> 1. 前者传递方式是传引用，即传入的实际值是原变量在内存中的地址
> 2. 后者传递方式是传引用，即传入的实际值是原变量在内存中的地址
> 3. 前者传递方式是传值，即传入的实际值是原变量的副本
> 4. 后者传递方式是传值，即传入的实际值是原变量的副本
>
> 为什么在函数 func 的参数后加上 & 会导致不同的输出？（单选）
>
> 1. & 会使相关变量在全局作用域被修改，从而导致两个内部参数不仅仅会在内部发生变化
> 2. & 传入两个变量内存中的位置，以此导致两者交换内存引用
> 3. 此处 & 使用有问题，不同引用在内存中被混淆了
> 4. 以上都不是
