# Python教程笔记

## Intro

Python本身是一个通用编程语言，但在一些库的加持下（numpy, pandas, mapotlib），他可以变身为强大的科学计算环境

对于有matlab使用经验的人，也可以用[numpy for matlab users](https://docs.scipy.org/doc/numpy-dev/user/numpy-for-matlab-users.html)

在此课程中包括：  

* 基本的Python:基本数据类型(容器Container、列表Lists、字典Dictionaries、集Sets、元组Tuples)、函数Functions、类Classes
* Numpy: 数组Arrays、数组索引Array indexing、数据类型Datatype、数组数学Array math、广播Broadcasting

## Python基础

Python版本查询：  

```python
python --version
```

Python允许用非常少的代码表达非常复杂的思想，被认为几乎像伪代码，这是Python实现快速排序算法的代码  

```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    # '//' means interger division
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x = pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)
print(quicksort([3,6,8,10,1,2,1]))
# 通过两个for循环形成嵌套
```

### 数据类型基础

#### 数

整型与浮点型与其他语言一样  
数据类型查询：

```Python
x=3
print(x,type(x))
```

计算符号

```python
print(x + 1)
print(x - 1)
print(x * 2)
print(x ** 2)
print(x / 2)
x += 1
print(x)
x *= 2
print(x)
```

注意：python没有自加自减符号(x++, x__)  
对于更多长整型、复杂数据类型，可参阅[文档](https://docs.python.org/3.7/library/stdtypes.html#numeric-types-int-float-long-complex)

#### 布尔运算

python使用英语而不是符号表示布尔运算符

```python
t, f = True, False
print(t and f)
print(t or f)
print(not f)
print(t != f)#不等运算符
```

#### 字符串

字符串的值可以使用单引号或双引号

```python
#String concatenation
hello = 'hello' + ' ' + 'world'
print(hello)
#String formatting
hw = '{} {} {}'.format(hello, world, 12)
print(hw)
```

字符串对象有许多操作，例如

```python
s = 'hello'
print(s.capitalize())#首字母大写
print(s.upper())#全大写
print(s.rjust(7))#右对齐，数字为行中字符数
print(s.center(7))#居中
print(s.replace('l','0'))#（查找某字符，全部替换为某字符）
print(' world '.strip())#（去掉字符前后空格）
```

所有的字符串操作参阅[文档](https://docs.python.org/3.7/library/stdtypes.html#string-methods)

### 容器

Python包括许多容器类型：列表Lists、词典Dictionaries、集Sets以及元组Tuples

#### 列表

python中的列表等同于数组，但是它可调整大小，并且可以包括不同类型的元素

```python
xs = [3, 1, 2]#创建列表
print(xs, xs[2])
print(xs[-1])# 负指数等同于从末尾开始数

xs[2] = 'foo'# 列表可以包含不同种类
print(xs)

xs.append('bar')# 在列表末尾加入元素
print(xs)

x = xs.pop()# 删除末尾元素
print(x, xs)
```

所有的列表操作参阅[文档](https://docs.python.org/3.7/tutorial/datastructures.html#more-on-lists)

#### Slicing

除了一次访问一个列表元素外，Python还提供了简洁的语法来访问子列表，这被称为切片

```python
nums = list(range(5)) #range用于创建一个整数列表
print(nums) #输出[0,1,2,3,4]
print(nums[2:4]) # 得到指数为2-4（不包括4）的子列表
print(nums[2:]) # 得到指数为2-末尾的子列表
print(nums[:2]) # 得到从开头到指数2（不包括）的子列表
print(nums[:]) # 得到整个列表的子列表
print(nums[:-1]) # 得到从开头到倒数第一个量的子列表
nums[2,4] = [8, 9] # 为子列表分配新的值
print(nums)
```

#### 循环

可以利用`for-in`循环遍历列表中的元素，缩进级别用于组织代码块  
缩进代码是`for`循环内部的

```python
animals = ['dogs', 'cats', 'monkey']
for animal in animals:
    print(animal)
```

为了访问循环体中每个元素的指数，使用内置的`enumerate`枚举函数,既有指数也有内容

```python
animals = ['dogs', 'human', 'whales']
for index, animal in enumerate(animals):
    print('{}. {}'.format(index + 1,animal))