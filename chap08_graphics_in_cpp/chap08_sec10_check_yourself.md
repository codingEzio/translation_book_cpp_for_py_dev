
### 8.10. 考考你自己
> 以下代码的撤销队列或有多大（即存储了多少个步骤）？（单选）
    >> 1. `13`
    >> 2. `10`
    >> 3. `8`
    >> 4. `4`
```cpp
#include <CTurtle.hpp>
namespace ct = cturtle;

int main() {
    ct::TurtleScreen screen;
    ct::Turtle turtle(screen);

    turtle.begin_fill();

    for(int i = 0; i < 4; i++){
        turtle.forward(50);
        turtle.right(90);
    }

    turtle.end_fill();

    screen.bye();
    return 0;
}
```

> 以下程序能够画出什么形状？（单选）
    >> 1. 圆形
    >> 2. 没有特定形状
    >> 3. 五角形
    >> 4. 星形
```cpp
#include <CTurtle.hpp>
namespace ct = cturtle;

int main() {
    ct::TurtleScreen screen;
    ct::Turtle turtle(screen);

    for(int i = 0; i < 5; i++){
        turtle.forward(50);
        turtle.right(144);
    }

    screen.bye();
    return 0;
}
```

> 同一个 `screen` 上可以有多个 `turtle` 对象（是否）
    >> 1. *True*
    >> 2. *False*
