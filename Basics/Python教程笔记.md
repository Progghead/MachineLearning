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

</br>

#### ***数***

</br>
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
</br>

#### ***布尔运算***

python使用英语而不是符号表示布尔运算符

```python
t, f = True, False
print(t and f)
print(t or f)
print(not f)
print(t != f)#不等运算符
```

#### ***字符串***

</br>
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
</br>

#### ***列表***

python中的列表等同于数组，但是它可调整大小，并且可以包括不同类型的元素

```python
xs = [3, 1, 2]#创建一个列表list
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

#### ***Slicing***  

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

#### ***循环***

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
```

#### ***列表解析-List Comprehensions***

编程的时候，我们经常会想要把一种类型数据转换成另一种，例如下面计算一组平方数的代码  

```python
nums = [0, 1, 2, 3, 4]
squares = []
for x in nums:
    squares.append(x ** 2)
print(squares)
```

利用列表解析可以使代码更简洁

```python
nums = [0, 1, 2, 3, 4]
squares = [x ** 2 for x in nums]
print(squares)
```

列表解析也可以包括条件判定

```python
nums = [0, 1, 2, 3, 4]
even_square = [x ** 2 for x in nums if x % 2 == 0]
print(even_square)
```

#### ***Dictionaries***

一个dictionary存储一对(键,值)，与javascript中的对象类似，下面是一个例子

```python
d = {'cat':'cute', 'dog':'furry'} #创建一个词典Dictionary，用大括号括住
print(d['cat']) #通过键来访问词典，得到值
print('cat' in d) # 键值是布尔量，可以检查词典是否有所给的键
```

```python
d['fish']='wet'
print(d.get('monkey', 'default')) 
#get函数负责查找键是否在字典里，如果存在就输出对应值，如果不在就输出后面默认值
print(d.get('fish', 'N/A'))
del d['fish']
print(d.get('fish', 'N/A'))
```

在词典中迭代键很容易

```python
d = {'person': 2, 'cat': 4, 'spider': 0}
for animal, legs in d.items():
# dicname.items()表示词典中所有键与值,不限制格式
    print('A {} has {} legs'. format(animal, legs))
```

词典解析：与列表解析类似，可以方便的创建列表，例如：

```python
nums = [0, 1, 2, 3, 4]
even_num_to_square = {x: x ** 2 for x in nums if x % 2 ==0}
# 从列表创建词典，加条件判定
```

词典的其他操作见[文档](https://docs.python.org/2/library/stdtypes.html#dict)

#### ***Sets***

Python中的集是不同元素的无序集合，

```python
animals = {'cats','dogs'} #创建一个集Set
print('cats' in animals) #检查元素是否在某个集里
print('fish' in animals)
animals.add('fish') #在集中加入新元素
print('fish' in animals)
print(len(animals)) #检查元素个数
```

```python
animals.add('cats') #在集中加入已有元素，不会改变集
print(len(animals))
animals.remove('cats') #在集中删除元素
print(len(animals))
```

遍历集合的语法和遍历列表的相同，但是由于集合是无序的，你无法预知你访问集合元素的顺序

```python
animals = {'cats', 'dogs', 'fishes'}
for idx, animal in enumerate(animals):
    print('{}'. {}, format(idx+1, animal)) # 运行结果的编号不会按照顺序
```

集合解析：利用集合解析方便的构建集合

```python
from math import sqrt
print({int(sqrt(x)) for x in range(30)}) 
 #把0-30的平方根取整后加入集合，重复元素不添加
 ```

#### ***Tuples***

元组是一个（不可变的）有序的值列表，它与列表最重要的区别在于

1. 元组可以用作词典中的键
2. 元组可以作为集合中的元素

```python
d = {(x, x + 1): x for x in range(10)} # 建立一个词典，其中元组作为词典的键
t = (5, 6) # 建立一个元组Tuple
print(type(t)) 
print(d[t]) # 通过键查找词典的值
print(d[(1, 2)])
```

### 函数

用`def`命令定义函数

```python
def sign(x):
    if x > 0:
        return 'positive'
    elif x < 0: # 用elif表示else if
        return 'negative'
    else
        return 'zero'

for x in [-1, 0, 1]:
    print(sign(x))
```

如何定义函数接受可选的关键字参数

```python
def hello(name, loud=false): # loud是可选参数，如果没有则默认为假
    if loud:
        print('HELLO, {}', format(name.upper()))
    else:
        print('Hello, {}', format(name))
```

### Classes 类

Python中定义类的语法很简单

```python
class Greeter:
    # 生成器
    def __init__(self, name): # self是参数，name是输入变量
        self.name = name #创建一个实例变量

    # 实例方法
    def greet(self, loud = false):
        if loud:
            print('HELLO, {}'.format(self.name.upper()))
        else:
            print('Hello, {}'.format(self.name))

g = Greeter('Fred') # 创建Greeter中的一个实例
g.greet() # 调用实例方法1
g.greet(loud = True) #调用实例方法2
```

## Numpy

Numpy是Python中科学计算的核心库。它提供了一个高性能的多维数组对象，以及用于处理这些数组的工具。

要使用Numpy，我们首先需要导入Numpy包，按照惯例，我们可以用别名`np`导入

```python
import numpy as np
```

### 数组

* numpy数组是由相同类型的值组成的*网格*，并由非负整数元组作为索引。
* 维数是数组的秩，数组的维度称为轴;
* 数组的形状shape是一个整数元组，给出了数组在每个维度上的大小。

创建一个一维数组

```python
a = np.array([1, 2, 3])
print(type(a), a.shape, a[0], a[1], a[2]) #输出数组类型，查看形状
a[0] = 5 #改变元素的值
print(a)
```

为了创建更多维数组，我们可以通过嵌套的方式

```python
b = np.array([[1,2],[3,4]]) # 创建一个二维数组
print(b)
print(b.shape)
c = np.array([[[1,2],[3,4]],[[5,6],[7,8]]])
print(c)
print(c.shape)
```

#### ***初始化数组***

numpy中初始化命令包括ones(), zeros(), random.random()等方法，我们只需要输入要求生成元素的个数

```python
a = np.zeros((2,2)) # 生成一个全为0的2*2数组
print(a)
b = np.ones((4,3,2)) # 生成一个全为1的4*3*2数组
print(b)
c = np.full((4,3,2), 7) # 生成一个全为7的数组
d = np.eye(2) # 生成一个2*2的单位矩阵
e = np.random.random((2,2)) # 生成全是随机数的矩阵
```

### 数组检索

1. 和列表切片一样，我们也可以将数组切片，得到想要的子数组，但多于1维的数组，需要确定每一维的切片范围

```python
a = np,array([[1,2,3,4],[5,6,7,8],[7,8,9,10]])
# 切出包括前两行第二列的数据
b = a[:2, 1] # 多于2维就不只是行和列，为此记住参数是从外向里生效就好
print(b)
# [[2]
# [6]]
```

子数组是同样数据的映射，因此改变它也将改变原有的数组

