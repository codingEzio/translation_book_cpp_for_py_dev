
### 8.8. 实际应用 - 平面填充 <small>(Tessellation)</small>
> 艺术的形式多种多样，从抽象到写实，并由极多各种不同类型的材料组成。古代苏美尔人将小块粘土染色并烘干，以创造出镶嵌画。这些镶嵌画通常由形状和图案组成，它们之间没有任何空隙。这种艺术形式今天被称为镶嵌艺术，你可以在任何由砖块组成的现代建筑或任何由瓷砖覆盖的地板上看到它的存在。不同的镶嵌艺术由其交错形状所变化，至于其媒介由何构成则因艺术家而异。
>
> 从尘土到木头，这种艺术形式的媒介随着时间的推移而变化。近代数字媒介已经被视为是物理媒介的一种很好的替代品。*Turtles* 即为这些数字媒介之一。你可以使用它创造各种具有重复或有规律性的图像。以下你的任务是用 *turtles* 制作一个风格类似于镶嵌画的方块图像。

> 以下是使用 C++ 的实现（*C-Turtle*）：
```cpp
#include <CTurtle.hpp>
namespace ct = cturtle;

int main() {
    const int SQUARE_SIZE = 35;

    ct::TurtleScreen screen;
    screen.tracer(0);  // 禁用动画效果

    ct::Turtle turtle(screen);

    turtle.speed(ct::TS_FASTEST);
    turtle.penup();

    for (int i = 0; i < 8; i++){
        turtle.goTo(
            -screen.window_width()  / 2,
            -screen.window_height() / 2 + (i * SQUARE_SIZE) + SQUARE_SIZE
        );

        bool is_blue = (i % 2 == 0);  // 偶数 (true) 或奇数(false) 行?

        for (int j = 0; j < 8; j++){
            ct::Color color;

            if (is_blue) {
                color = {"blue"};
            }
            else {
                color = {"orange"};
            }

            turtle.begin_fill();
            turtle.fillcolor(color);

            for(int i = 0; i < 4; i++){
                turtle.forward(SQUARE_SIZE);
                turtle.right(90);
            }

            turtle.end_fill();

            turtle.forward(SQUARE_SIZE);
            is_blue = !is_blue;  // 在 true 与 false 之间翻转
        }
    }

    screen.bye();

    return 0;
}
```

> 这个使用的是 Python 中的 *turtle*，其功能与以上程序相同：
```python
import turtle

SQUARE_SIZE = 35

wn = turtle.Screen()
wn.tracer(0)
square = turtle.Turtle()

square.speed(10)

square.penup()
square.goto(-turtle.window_width() / 2, turtle.window_height() / 2)
square.pendown()


a = 0
b = 0

for i in range(8):
    if b == 0:
        a = 1
    else:
        a = 0

    for j in range(8):
        square.penup()
        square.goto(
            -turtle.window_width() / 2 + j * SQUARE_SIZE,
            (-turtle.window_height() / 2) + i * SQUARE_SIZE + SQUARE_SIZE,
        )
        square.pendown()

        if a == 0:
            square.fillcolor("orange")
            a = 1
        else:
            square.fillcolor("blue")
            a = 0

        square.begin_fill()

        for k in range(4):
            square.forward(SQUARE_SIZE)
            square.right(90)

        square.end_fill()

    if b == 0:
        b = 1
    else:
        b = 0

wn.tracer(1)
```

> 现在来实践下你所学习的知识吧。你的实现必须遵循如下需求：
>
> 1. 你选择的形状中不能有四个边缘（即矩形），但 3 边或 5 边以上没有问题。
> 2. 图像中的形状不超过两种颜色。

```cpp
#include <CTurtle.hpp>
namespace ct = cturtle;

int main() {
    ct::TurtleScreen scr;
    scr.tracer(0);  // 禁用动画效果
    ct::Turtle turtle(scr);

    // 在这里放置你的代码

    scr.bye();
    return 0;
}
```
