# Python学习笔记

[TOC]

## 运行环境

### 关于命令行模式

在终端中，输入`python`即可进入python命令行模式，输入`exit()`退出python命令行模式。

### 关于缩进

python格式一个特点就是使用缩进作为一个域的标识，比如下面这个例子：

```python
sum = 0
n = 99
while n > 0:
    sum = sum + n
    n = n - 2
print(sum)
```

如果第5行不缩进，那`while`语句块就不把这行代码包揽进去，这是Python的缺点之一。

## Python基础

### 输入和输出

#### 输入

```python
print('The quick brown fox', 'jumps over', 'the lazy dog')
```

1. 打印函数基本格式是`print()`，使用`''`包住字符串；
2. `print()`函数也可以接受多个字符串，用逗号“,”隔开，遇到逗号“,”会输出一个**空格**；
3. `print()`也可以打印整数，或者计算结果

#### 输出

```python
>>> name = input()
czc
>>> name
'czc'
```

```python
>>> name = input('please enter your name: ')
please enter your name: czc
>>> name
'czc'
```

```python
>>> name = input()
1234
>>> name
'1234'
```

可以看到，`input()`可以带提示字符串进行输入，但其返回值只能是字符串，无法返回数。

### 数据类型和变量

#### 整数

1. 对于很大的数，Python允许使用`_`进行分割，如：`10_000_000_000`和`10000000000`是完全一样的。十六进制数也可以写成`0xa1b2_c3d4`。

#### 字符串

1. 字符串可以使用单引号`'`或双引号`"`括起来，两种都可以。
1. 如果`'`本身也是一个字符，那就可以用`""`括起来。
1. 如果包含`"`，可以使用转义字符`\`来标识。
1. 可以用`\n`表示换行，`\t`表示制表符
1. Python还允许用`r''`表示`''`内部的字符串默认不转义
1. 如果字符串内部有很多换行，用`\n`写在一行里不好阅读，为了简化，Python允许用`'''...'''`的格式表示多行内容

根据以上规则，以下表达式对应字符内容如下：

| ①    | "I'm OK"       | I'm OK    |
| ---- | -------------- | --------- |
| ②    | 'I\'m \"OK\"!' | I'm "OK"! |
| ③    | '\\\t\\'       | \       \ |
| ④    | r'\\\t\\'      | \\\t\\    |

#### 布尔值

Python允许使用`True`、`False`两种布尔值，注意大小写。

另外还可以使用`and`、`or`和`not`运算。

#### 空值（None）

`None`是一个特殊的空值，不能理解为`0`

#### 地板除（//）

在Python中除了`/`，还有一种除法是`//`，称为地板除，特点是取整数部分，舍去所有小数部分。

#### 字符和字符串

Python提供了`ord()`函数获取字符的整数表示，`chr()`函数把编码转换为对应的字符，例如：

```python
>>> ord('A')
65
>>> ord('中')
20013
>>> chr(66)
'B'
>>> chr(25991)
'文'
>>> '\u4e2d\u6587'
'中文'
```

#### 格式化

Python的格式化与C语言类似，例如：

```Python
>>> 'Hello, %s' % 'world'
'Hello, world'
>>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
'Hi, Michael, you have $1000000.'
```

| 占位符 | 替换内容     |
| ------ | ------------ |
| %d     | 整数         |
| %f     | 浮点数       |
| %s     | 字符串       |
| %x     | 十六进制整数 |

> 1. `%s`可以将任意数据类型转换为字符串，是万能的；
> 2. 当`%`作为一个普通字符时，用`%%`来表示一个`%`
> 3. 还有一种格式化方法是使用`format()`[方法](https://www.liaoxuefeng.com/wiki/1016959663602400/1017075323632896)
> 4. 最后还有一种格式化字符串的方法是使用以`f`开头的字符串，称之为`f-string`，参考[这里](https://www.liaoxuefeng.com/wiki/1016959663602400/1017075323632896)

#### list and tuple

`list`是一种有序的集合，其语法格式如下：

```python
>>> classmates = ['Michael', 'Bob', 'Tracy']
```

1. 可用索引来访问list中每一个位置的元素，记得索引是从`0`开始的，例如：`classmates[0]`

2. 如果要取最后一个元素，除了计算索引位置外，还可以用`-1`做索引，直接获取最后一个元素，以此类推，可以获取倒数第2个、倒数第3个。

   ```python
   >>> classmates[-1]
   'Tracy'
   >>> classmates[-2]
   'Bob'
   >>> classmates[-3]
   'Michael'
   >>> classmates[-4]
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
   IndexError: list index out of range
   ```

3. 另外还可以追加，插入，删尾，剔除，替换元素。

   ```python
   classmates.append('Adam') # 追加
   classmates.insert(1, 'Jack')# 插入
   classmates.pop() # 删尾
   classmates.pop(1) # 剔除
   classmates[1] = 'Sarah' # 替换
   ```

4. list里面的元素的数据类型也可以不同，可以是另一个list

   ```python
   L = ['Apple', 123, True]
   s = ['python', 'java', ['asp', 'php'], 'scheme']
   
   p = ['asp', 'php']
   s = ['python', 'java', p, 'scheme']
   ```

​		上面这种嵌套可以看作一个二维数组，对于``'php'``这		个元素可以写`p[1]`或者`s[2][1]`。

`tuple`是另外一种有序列表，其格式如下：

```python
>>> classmates = ('Michael', 'Bob', 'Tracy')
```

1. 它与list的区别在于一旦一开始定义好了，后面就不能变了，它也没有append()，insert()这样的方法，其他获取元素的方法和list是一样的，你可以正常地使用`classmates[0]`，`classmates[-1]`，但不能赋值成另外的元素。因为tuple不可变，所以代码**更安全**。如果可能，能用tuple代替list就**尽量用tuple**。

> ⚠︎ tuple的陷阱:
>
> 当你定义一个tuple时，在定义的时候，tuple的元素就必须被确定下来，比如：
>
> ```python
> >>> t = (1, 2)
> >>> t
> (1, 2)
> ```
>
> 如果要定义一个空的tuple，可以写成`()`：
>
> ```python
> >>> t = ()
> >>> t
> ()
> ```
>
> 但是，要定义一个只有1个元素的tuple，如果你这么定义：
>
> ```python
> >>> t = (1)
> >>> t
> 1
> ```
>
> 定义的不是tuple，是`1`这个数！
>
> 这是因为括号`()`既可以表示tuple，又可以表示数学公式中的小括号，这就产生了歧义，因此，Python规定，这种情况下，按小括号进行计算，计算结果自然是`1`。
>
> 所以，只有1个元素的tuple定义时必须加一个逗号`,`，来消除歧义：
>
> ```python
> >>> t = (1,)
> >>> t
> (1,)
> ```

2. 另外还有一种tuple嵌套list

   ```python
   >>> t = ('a', 'b', ['A', 'B'])
   ```

   这种在`t`中可以修改list里`'A'`和`'B'`两个元素的值，其原因不言自明。

### 条件判断

关于条件判断，基本用法和C差不多，主要在格式和关键词（elif）上的差别：

```python
age = 20
if age >= 6:
    print('teenager')
elif age >= 18:
    print('adult')
else:
    print('kid')
    
if x:
    print('True')
```

> ⚠︎ 关于input ⚠︎
>
> ```python
> birth = input('birth: ')
> if birth < 2000:
>     print('00前')
> else:
>     print('00后')
> ```
>
> 输入`1999`后会报错：
>
> ```visual basic
> Traceback (most recent call last):
>   File "<stdin>", line 1, in <module>
> TypeError: unorderable types: str() > int()
> ```
>
> 这是因为`input()`返回的数据类型是`str`，`str`不能直接和整数比较，必须先把`str`转换成整数。Python提供了`int()`函数来完成这件事情：
>
> ```python
> s = input('birth: ')
> birth = int(s)
> if birth < 2000:
>     print('00前')
> else:
>     print('00后')
> ```
>
> 这和直接比较比较式不同的：
>
> ```python
> birthyear = 1999
> if birthyear < 2000:
>     print('you are after 90.')
> else:
>     print('you are after 00')
> ```

### 循环

#### for...in循环

```python
names = ['Michael', 'Bob', 'Tracy']
for name in names:
    print(name)
```

上面的代码意思就是把`names`里的所有元素依次带入`name`这个变量中，并依次打印出来。

#### range

python提供了一个`range()`函数，可以生成一个整数列，再通过`list()`就可以转换为list。

注意对于`range(n)`是生成从0开始，到(n-1)结束的整数列

```python
>>> list(range(5))
[0, 1, 2, 3, 4]
```

#### while循环

基本用法和C相同，格式如下：

```Python
sum = 0
n = 99
while n > 0:
    sum = sum + n
    n = n - 2
print(sum)
```

#### break 和 continue

两个使用方法和C相同

#### 退出程序

使用`Ctrl`+`C`可以退出程序，如果陷入死循环之类就可以使用这个处理。

### dict 和 set

#### dict

Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。

以下为一个例子：

```python
>>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
>>> d['Michael']
95
```

把数据放入dict的方法，除了初始化时指定外，还可以通过key放入：

```python
>>> d['Adam'] = 67
>>> d['Adam']
67
```

1. 由于一个key只能对应一个value，所以，多次对一个key放入value，后面的值会把前面的值冲掉

2. 要避免key不存在的错误，有两种办法，一是通过`in`判断key是否存在

   ```python
   >>> 'Thomas' in d
   False
   ```

   二是通过dict提供的`get()`方法，如果key不存在，可以返回`None`，或者自己指定的value

   ```python
   >>> d.get('Thomas') # 这里返回None，在终端上不显示结果
   >>> d.get('Thomas', -1)
   -1
   ```

3. 要删除一个key，用`pop(key)`方法，对应的value也会从dict中删除：

   ```python
   >>> d.pop('Bob')
   75
   >>> d
   {'Michael': 95, 'Tracy': 85}
   ```

> ⚠︎ 由于dict需要通过哈希算法计算一个确定的值，key就不能是变量，不然就混乱了

#### set

set具有如下特点：

1. set和dict类似，也是一组key的集合，但不存储value。
2. 由于key不能重复，所以，在set中，没有重复的key。
3. set中并不存在“序”。

```python
# 创建一个set
>>> s = set([1, 2, 3])
>>> s
{1, 2, 3}>>> s = set([1, 2, 3])
>>> s
{1, 2, 3}
```

4. 重复元素在set中自动被过滤：

   ```python
   >>> s = set([1, 1, 2, 2, 3, 3])
   >>> s
   {1, 2, 3}
   ```

5. 通过`add(key)`方法可以添加元素到set中，可以重复添加，但不会有效果.

6. 通过`remove(key)`方法可以删除元素。

7. set可以看成数学意义上的无序和无重复元素的集合，因此，两个set可以做数学意义上的交集、并集等操作：

   ```python
   >>> s1 = set([1, 2, 3])
   >>> s2 = set([2, 3, 4])
   >>> s1 & s2
   {2, 3}
   >>> s1 | s2
   {1, 2, 3, 4}
   ```

8. set同样不能储存可变对象

> 不可变对象
>
> 这里举两个例子，一个是可变对象list，一个是不可变对象str，来对比一下两个的差别
>
> 对于list，使用排序方法`sort()`：
>
> ```python
> >>> a = ['c', 'b', 'a']
> >>> a.sort()
> >>> a
> ['a', 'b', 'c'] # 可以看见顺序变了
> ```
>
> 对于str，使用替换方法`replace()`：
>
> ```python
> >>> a = 'abc'
> >>> a.replace('a', 'A')
> 'Abc'
> >>> a
> 'abc' # 实际变量a并没有变化
> ```
>
> 可以发现，对于str，调用·`replace()`其实是作用于`a`所指向的字符串本身`'abc'`的，然后返回一个新字符串，而对于原来的的`'abc'`，并没有进行修改。所以只能使用一个姓的变量来指向这个新的变量。
>
> ```tex
> ┌───┐                  ┌───────┐
> │ a │─────────────────>│ 'abc' │
> └───┘                  └───────┘
> ┌───┐                  ┌───────┐
> │ b │─────────────────>│ 'Abc' │
> └───┘                  └───────┘
> ```

## 函数

### 调用函数

Python内置函数可以看[官方文档](http://docs.python.org/3/library/functions.html#abs)

> 可以使用`help(abs)`来查看帮助

#### 数据类型转换

Python内置的常用函数还包括数据类型转换函数：

```python
>>> int('123')
123
>>> int(12.34)
12
>>> float('12.34')
12.34
>>> str(1.23)
'1.23'
>>> str(100)
'100'
>>> bool(1)
True
>>> bool('')
False
```

<u>函数名其实就是指向一个函数对象的引用</u>，完全可以把函数名赋给一个变量，相当于给这个函数起了一个“别名”：

```python
>>> a = abs # 变量a指向abs函数
>>> a(-1) # 所以也可以通过a调用abs函数
1
```

### 定义函数

基本格式如下：

```txt
┌────────────────────────────────┐
│Command Prompt - python   - □ x │
├────────────────────────────────┤
│>>> def my_abs(x):              │
│...     if x >= 0:              │
│...         return x            │
│...     else:                   │
│...         return -x           │
│...                             │
│>>> my_abs(-9)                  │
│9                               │
│>>> _                           │
│                                │
│                                │
└────────────────────────────────┘
```

> ⚠︎ 在Python交互环境中定义函数时，注意Python会出现`...`的提示。函数定义结束后需要按两次回车重新回到`>>>`提示符

如果你已经把`my_abs()`的函数定义保存为`abstest.py`文件了，那么，可以在该文件的当前目录下启动Python解释器，用`from abstest import my_abs`来导入`my_abs()`函数，注意`abstest`是文件名（不含`.py`扩展名）：

```angelscript
┌──────────────────────────────────────────┐
│Command Prompt - python             - □ x │
├──────────────────────────────────────────┤
│>>> from abstest import my_abs            │
│>>> my_abs(-9)                            │
│9                                         │
│>>> _                                     │
│                                          │
│                                          │
│                                          │
│                                          │
│                                          │
│                                          │
│                                          │
└──────────────────────────────────────────┘
```

### 空函数

如果想定义一个什么事也不做的空函数，可以用`pass`语句：

```python
def nop():
    pass

# 可以用在其他语句中
if age >= 18:
    pass
```

### 参数检查

我们可以在函数中添加参数类型检查，从而抛出错误。例如`my_abs`函数的检查：

```python
def my_abs(x):
    if not isinstance(x, (int, float)):
        raise TypeError('bad operand type')
    if x >= 0:
        return x
    else:
        return -x
```

添加了参数检查后，如果传入错误的参数类型，函数就可以抛出一个错误：

```python
>>> my_abs('A')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 3, in my_abs
TypeError: bad operand type
```

### 返回多个值









