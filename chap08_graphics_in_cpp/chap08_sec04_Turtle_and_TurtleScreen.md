
### 8.4. `Turtle` 与 `TurtleScreen`
> 你需要先创建一个 "画板"，之后才能在上面绘制 `Turtle`。这个与 Python 格外不同，你需要先创建一个 screen（即 `TurtleScreen`），然后再创建 `Turtle` 对象（此处为 `turtle`）。
```cpp
ct::TurtleScreen screen;
ct::Turtle       turtle(screen);  // 注意到我们将 screen 对象传给了 turtle() 函数
```

> 关闭 `TurtleScreen` 的方式与 Python 里一致，不过在此章节我们将只使用 `bye`。你并非必须使用 `bye` 方法：其他退出方法的实现依然会使用 `bye`。另外，即使你不使用任何退出方法，*Turtle* 在绘制完毕后会自动关闭。`exitonclick` 也是针对 `bye` 很好的一个替代品，它在你点击后才会退出。
```cpp
screen.bye();
```

> *Turtles* 代表的是：在画布上有一只海龟，它的尾部带有彩色的笔。此处的 "画布" 即为 `TurtleScreen`。这个 "海龟" 会听从你任何给它的指令，包括往特定方向前进、使用哪种颜色的笔，以及何时抬起或落下画笔等等。以下是一些常用的指令：
>
| 方法名             | 描述                                                        |
| :----------------- | :---------------------------------------------------------- |
| `turtle.left`      | 海龟左转 *N* 度 (可改配置，改接收弧度)                      |
| `turtle.right`     | 海龟右转 *N* 度 (可改配置，改接收弧度)                      |
| `turtle.penup`     | 画笔抬起，移动时不画线                                      |
| `turtle.pendown`   | 画笔落下，移动时将画线                                      |
| `turtle.fillcolor` | 返回或设置填充颜色                                          |
| `turtle.beginfill` | 在绘制要填充的形状之前调用                                  |
| `turtle.endfill`   | 填充上次调用 `begin_fill()` 之后绘制的形状                  |
| `turtle.pencolor`  | 返回或设置画笔颜色                                          |
| `turtle.width`     | 设置线条的粗细为 *N* 或返回该值                             |
| `turtle.speed`     | 设置移动速度为 0 至 10（除 0 之外，数字越大，绘制速度越快） |
| `turtle.back`      | 海龟后退 *N* 距离（方向与海龟的朝向相反；不改变朝向）       |
| `turtle.forward`   | 海龟前进 *N* 距离（方向为海龟的朝向）                       |
| `turtle.goto`      | 海龟移动到指定的绝对坐标处                                  |
| `turtle.write`     | 基于给定参数写文本至海龟当前所在位置                        |

> 你可以混用以上多个命令来绘制出不同的图像。*C-Turtle* 里也可以像 *turtle* 那样调整速度。速度值为 0 到 10 之间的整数，除去 0 之外（*极快*），数字越大，速度越快。以下的前缀 `TS` 代表 "*T*urtle *S*peed"。
>
| Python *turtle* | C++ *C-Turtle* | 速度值 |
| :-------------- | :------------- | :----- |
| `"fastest"`     | `TS_FASTEST`   | 0      |
| `"fast"`        | `TS_FAST`      | 10     |
| `"normal"`      | `TS_NORMAL`    | 6      |
| `"slow"`        | `TS_SLOW`      | 3      |
| `"slowest"`     | `TS_SLOWEST`   | 1      |

> 来看个有详细标注的程序：
```cpp
#include <CTurtle.hpp>
namespace ct = cturtle;

int main() {
    // 创建一个 turtle screen, 并将我们的 screen 传进 turtle
    ct::TurtleScreen screen;
    ct::Turtle turtle(screen);

    // 将速度调整到最慢
    turtle.speed(ct::TS_SLOWEST);
    // 任何 0 至 10 之间的整数均可，比如:
    // turtle.speed(7);

    // 将填充颜色设置为紫色
    turtle.fillcolor({"purple"});

    // 开始填充
    turtle.begin_fill();

    // 使用 turtle 绘制一个正方形

    // 在每一角处循环以下的代码块
    for (int i = 0; i < 4; i++) {

        // 让 turtle 往前移动 50 单位
        turtle.forward(50);

        // 让 turtle 右转 90 度
        turtle.right(90);
    }

    // 停止填充
    turtle.end_fill();

    // 关闭 turtle screen
    screen.bye();
    return 0;
}
```

> 以上代码绘制出的是一个在中央的紫色的正方形。如果你有在 Python 里使用 *turtle* 的话，这些对你来说应该完全是不在话下的。如果你没有使用过，那也没有关系，我们在此后的章节中会更详细地介绍它们。
>
> 以上不同命令的给定顺序十分重要，有些指令必须在其他指令之前或之后进行。比如 `begin_fill` 和 `end_fill`，你只有在这两者之间加入指令才能绘制出你想要的形状。
