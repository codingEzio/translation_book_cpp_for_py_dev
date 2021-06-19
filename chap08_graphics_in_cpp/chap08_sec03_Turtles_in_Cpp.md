
### 8.3. C++ 里的 *Turtle*
> 鉴于其开箱即用以及具有优秀文档的特性，Python 特别适合用于教育领域。这些都是 C++ 的薄弱点：就算是只使用一些自带的工具都需要理解其相对复杂的语法，以及了解 C++ 是如何运作的。我们这里的提到的 *turtle* 库就能够提供诸多能够辅助教育的特性：动态、可交互，以及你能够从视觉上看到代码逻辑是怎样在运作的。
>
> 这种可视化为学生们提供了从一个新的看待计算机科学的角度：与其进行枯燥无味的 `print`，你能够直接看到可视化的概念。这个在学习较为抽象的概念时格外有用，比如递归和迭代。
>
> C++ 里也有一个对等的库：*C-Turtle*，它简单易用，并且与 Python *turtle* 里的对象和指令大体一致。它由隶属贝里亚学院 <small>(Berea College)</small> 的 *Jesse Walker-Schadler* 在 2019 年夏季开发的，你可以在 Github 上找到此项目：[https://github.com/walkerje/C-Turtle](https://github.com/walkerje/C-Turtle)。

> 以下是两个版本的对比。你可以尝试运行下两者，看看有什么区别。
```cpp
#include <CTurtle.hpp>
namespace ct = cturtle;

int main() {
    ct::TurtleScreen scr;
    ct::Turtle turtle(scr);

    turtle.speed(ct::TS_SLOWEST);
    turtle.fillcolor({"purple"});

    turtle.begin_fill();

    for (int i = 0; i < 4; i++) {
        turtle.forward(50);
        turtle.right(90);
    }

    turtle.end_fill();

    scr.bye();

    return 0;
}

```

```python
import turtle


turt = turtle.Turtle()

turt.fillcolor("purple")
turt.speed("slowest")

turt.begin_fill()

for i in range(4):
    turt.forward(50)
    turt.right(90)

turt.end_fill()
```

> C-Turtle 这种可视化的库对学生的益处有哪些？（多选）
>
> 1. 学生们能够得到即刻反馈以及完成任务的满足感
> 2. 学生们会不再把注意力放在如何读懂代码，而是只关注结果了
> 3. 学生们能够更熟悉网站开发中 RGB 颜色常用值
> 4. 学生们能够更自如地学习自己熟悉的东西，比如 *Turtles*
