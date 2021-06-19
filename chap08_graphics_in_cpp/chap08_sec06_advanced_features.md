
### 8.6. 进阶功能
> *Turtles* 这个工具并不小，并且其中有许多选项能够改变它是如何运作的。有些与 *turtles* 内部运作相关的指令就是要比普通的要复杂些，比如 `tracer`、`undo` 以及 `screen` 的不同模式 `mode`。

> 海龟模式用于设定从哪边来测量角度。根据 `TurtleScreen` 的不同模式，为正数的角度既可能是顺时针的，也可能是逆时针的。你可以使用 `mode` 方法来调整它：
>
>
| 模式          | 初始海龟朝向 | 正数角度 |
| :------------ | :----------- | :------- |
| `SM_STANDARD` | 朝右 (东)    | 逆时针   |
| `SM_LOGO`     | 朝上 (北)    | 顺时针   |

> *Turtles* 在进行旋转时既可使用角度，也可使用弧度。你可以通过 `radians` 和 `degrees` 两个方法来调整不同度数体系，默认体系为 *度*。这些改变只会影响两个方向的方法，即 `left` 和 `right`。
```cpp
turtle.degrees();
turtle.right(90);       // 往右旋转 90 度

turtle.radians();
turtle.left(1.5708f);   // 往左旋转 1.5708 弧度 (约等于 90.0002 度)
```

> `tracer(N)` 方法用于设置海龟动画刷新图形的延迟时间。此方法隶属于 `TurtleScreen` 对象，所以改变相关数值后，所有的 `turtle` 实例对象都会被影响到。这里的 `N` 用于指定 `TurtleScreen` 每 *N* 帧显示刷新一次动画。

> `tracer` 可与 `speed` 方法一同使用非常快速地绘制出图像。`speed` 的最大值 `TS_FASTEST` 可以将在移动旋转之间的动画效果完全禁止掉。如此，`tracer` 方法就能够完全实现每多少次移动才显示一次动画。当然了，虽然你看不到动画，但那些移动确实是进行了。
```cpp
screen.tracer(3);               // 每 3 次移动显示一帧动画。
turtle.speed(ct::TS_FASTEST);   // 完全禁止移动旋转之间的动画效果

turtle.forward(50);             // 这个动画不会被体现出来
turtle.right(90);               // 这个也不会...
turtle.forward(50);             // 这个会，因为它是第三次移动
```

> 不管是处于移动还是静止状态，每一个移动 <small>(action)</small> 都会被插入一帧。这包括类似 `begin_fill`、`end_fill` 这样的方法，虽然它不绘制任何东西，但其在背后会告诉 *turtle* 何时开始或停止追踪自己的移动。
>
> 理解以下程序并回答相关问题。
```cpp
#include <CTurtle.hpp>
namespace ct = cturtle;

int main(){
    ct::TurtleScreen screen;
    ct::Turtle turtle(screen);

    turtle.speed(ct::TS_FASTEST);
    screen.tracer(6);

    for(int i = 0; i < 3; i++){
        turtle.right(60);
        turtle.forward(50);
    }

    screen.bye();

    return 0;
}
```

> 以上程序运行后会有多少帧的动画？（单选）
>
> 1. `3`
> 2. `6`
> 3. `1`
> 4. `12`

> 类似 `tracer` 的设定，每一次 `turtle` 的移动都会被追加到一个撤销队列 <small>(`undo queue`)</small> 中。由此你可以记录其每一次的移动轨迹。此队列默认值为 `100`，你可以通过 `setundobuffer` 方法来修改。即使没有绘制任何图像的也会被记录。这里的 "撤销" 类似于多数文本编辑器里的撤销。你可以通过 `undo` 方法来撤销 *N* 步的进度。

> 以上程序运行后，其撤销队列中存储了多少个移动指令？（单选）
>
> 1. `3`
> 2. `6`
> 3. `1`
> 4. `12`
