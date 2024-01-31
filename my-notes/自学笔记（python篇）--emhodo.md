----
2024/01/31
昨天重新发现这篇教程，于是重新回想起了当初打算自学python的想法。我虽然也不算是新手了，但python很多语法和其他不一样，所以我打算再仔细学一下。目前学到流程控制。有了以下认识：

1. python里条件判断可以不需要括号
2. `bool`类型变量需要首字母大写
3. 变量类型好像是自动转换，只有在必要的情况下需要手动转换
4. 空变量用的标识是`None`而不是`null`

在章节末的骰子游戏我也简单做了一下：
```python
import random


def clamp(value, min_value, max_value):
    return max(min(value, max_value), min_value)


def main(arg):
    print("welcome to coin game!")
    fina_player = 10
    fina_robot = 10
    while True:
        dice_num = random.randint(2, 12)
        print('input \'b\' to guess large')
        print('input \'r\' to guess small')
        print('input \'q\' to quit the game')
        user_input = input("input:>>")
        if user_input == 'q':
            break
        else:
            result = judge(dice_num, user_input)
            fina_player = fina_player + result
            fina_player = clamp(fina_player, 0, 10)
            fina_robot = fina_robot - result
            fina_robot = clamp(fina_robot, 0, 10)
        print("your score is " + str(fina_player))
        print("the robot score is " + str(fina_robot))
        if fina_player == 0:
            print("game over, the winner is robot")
        elif fina_robot == 0:
            print("game over, the winner is player")


def judge(dictum, user_input):
    if dictum == 7:
        print("Draw!")
        return 0
    if dictum < 7:
        if user_input == 'b':
            print("You lost!")
            return -1
        else:
            print("You win!")
            return 1
    if dictum > 7:
        if user_input == 'b':
            print("You win!")
            return 1
        else:
            print("You lost!")
            return -1


if __name__ == '__main__':
    main(None)


```

到函数这部分，学到最多的还是如何阅读官方文档的函数参数的构成，这对我来说几乎是全新的。

> - **位置参数**（Positional Arguments，在官方文档里常被缩写为 *arg*）也就是除了关键字参数以外的参数
> - **关键字参数**（Keyword Arguments，在官方文档里常被缩写为 *kwarg*）被赋予默认值的参数
> - **`[]`** 包裹住一个参数，表示可选参数
> - **`*`** 放在参数前面，表示可以接受多个参数（列表）

在后面还出现了一个`class`函数，这是啥？感觉不像类啊

强制转换是使用类型加`()`，也就是以函数的形式进行转换
