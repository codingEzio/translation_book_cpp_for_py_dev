
### 4.3. 传入数组
> 集合数据类型中的数组是 Python 中 列表 <small>(list)</small> 的鼻祖，我们将在之后的章节中进行更深入地讲解。将数组作为函数参数与我们以往的传值、传引用完全不同。单从其定义以及参数来看的话，它确实看起来很像之前提到的 “传值”，至于其变量名则是多了一组中括号 `[]`。

> 以下函数通过循环接收的数组计算出其平均值：
```cpp
double average(int list[], int length) { // []不指定数组长度是符合语法的
    double total = 0;
    int count;

    for( count = 0; count < length; count++ ) {
        total += double(list[count]);
    };

    return (total / length);
}
```

> 数组参数从语法上看很像传值，但在实际运作上它更像是传引用。当函数运行时，相应参数并不会被重新复制一遍，实际被传入的是数组的引用，这样在一定程度上能够减少内存的使用量。简单地说，当你将数组传入函数时，其值能够被函数内的逻辑永远改变。

> 调用以下函数后，第三个数组参数内的每个元素将会是第一第二个对应元素的总和：
```cpp
void add_lists(int first[], int second[], int total[], int length) {
    int count;

    for (count = 0; count < length; count++) {
        total[count] = first[count] + second[count];
    }
}
```

> 从以上程序我们可以看到我们并没有修改第一第二个数组的需求，为了避免误操作，我们可以在其类型前加上关键词 `const`：
```cpp
void add_lists(const int first[], const int second[], int total[], int length) {
    int count;

    for (count = 0; count < length; count++) {
        total[count] = first[count] + second[count];
    }
}
```

> 以上函数参数内的 `const` 能够保证未来任何对相应参数的修改都能立即被编译器阻止。
