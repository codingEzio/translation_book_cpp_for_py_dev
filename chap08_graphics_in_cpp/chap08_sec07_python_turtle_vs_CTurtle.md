
### 8.7. Python 自带的 *turtle* 与 *C-Turtle*
> 它们两者的差别主要是在语法上。多数方法在具体实现上完全相同，不过也有一些小小的例外。颜色名在 C-Turtle 里必须由花括号 `{}` 裹住（如 `{"red"}`）。另外，你还能够 `{"random"}` 指定一个随机的颜色。
```cpp
ct::Color red   = {"red"};
ct::Color green = {"green"};
ct::Color blue  = {"blue"};
ct::Color random = {"random"};

// 你可以这样使用
turtle.pencolor(red);

// 也可以直接这样
turtle.pencolor({"green"});
turtle.pencolor({"random"});
```

> 与 Python 里的 *turtle* 不同，*C-Turtle* 里的 `write` 方法无法指定字体或字体大小名，这是因为在 C++ 里操作字体非常地复杂。另外，这个库里也没有 Python 里 screen 的 "*world*" 模式。这个模式可以用于规定画板的边界，比如坐标的最大值和最小值。
>
> 默认形状的可选择的空间也比较有限。Python 的 *turtle* 提供有六个默认形状，即 `arrow`、`circle`、`turtle`、`square`、`triangle` 以及 `classic`；*C-Turtle* 则只提供了四种：`arrow`、`triangle`、`indented_triangle` 以及 `square`。

> *C-Turtle* 里也有一些 Python *turtle* 里没有的实用小工具，比如 `shift`、`middle`。前者可用于与原所在处的坐标运算，如果你当前在 `600x, 400y`，那么当你调用 `50x, -50y` 之后，你的位置会被转移到 `650x, 350y`。后者（即 `middle`）则会返回两坐标的中心点。
```cpp
turtle.goTo(600, 400);
turtle.shift(50, -50);
// 现在 Turtle 的位置在坐标 650x, 350y

ct::Point a = {400, 300};
ct::Point b = {450, 300};

// 其结果应为 425x, 300y (两座标的中心点)
ct::Point middle = ct::middle(a, b);
```
