<div align="center">
  <h1> 🐍 30 Days Of Python：第 14 天 - 高阶函数（Higher Order Functions）</h1>
  <a class="header-badge" target="_blank" href="https://www.linkedin.com/in/asabeneh/">
  <img src="https://img.shields.io/badge/style--5eba00.svg?label=LinkedIn&logo=linkedin&style=social">
  </a>
  <a class="header-badge" target="_blank" href="https://twitter.com/Asabeneh">
  <img alt="Twitter Follow" src="https://img.shields.io/twitter/follow/asabeneh?style=social">
  </a>

  <sub>作者（Author）：
  <a href="https://www.linkedin.com/in/asabeneh/" target="_blank">Asabeneh Yetayeh</a><br>
  <small>第二版（Second Edition）：2021 年 7 月</small>
  </sub>

</div>

[<< 第 13 天](../13_Day_List_comprehension_列表推导式/13_list_comprehension_列表推导式.md) | [第 15 天 >>](../15_Day_Python_type_errors_类型错误/15_python_type_errors_Python类型错误.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)
- [📘 第 14 天](#-第-14-天)
  - [高阶函数（Higher Order Functions）](#高阶函数higher-order-functions)
    - [函数作为参数](#函数作为参数)
    - [函数作为返回值](#函数作为返回值)
  - [Python 闭包（Closures）](#python-闭包closures)
  - [Python 装饰器（Decorators）](#python-装饰器decorators)
    - [创建装饰器](#创建装饰器)
    - [将多个装饰器应用于单个函数](#将多个装饰器应用于单个函数)
    - [在装饰器函数中接受参数](#在装饰器函数中接受参数)
  - [内置高阶函数](#内置高阶函数)
    - [Python - Map 函数](#python---map-函数)
    - [Python - Filter 函数](#python---filter-函数)
    - [Python - Reduce 函数](#python---reduce-函数)
  - [💻 练习：第 14 天](#-练习第-14-天)
    - [练习：第 1 级](#练习第-1-级)
    - [练习：第 2 级](#练习第-2-级)
    - [练习：第 3 级](#练习第-3-级)

# 📘 第 14 天

## 高阶函数（Higher Order Functions）

在 Python 中，函数被视为一等公民（first class citizens），允许你对函数执行以下操作：

- 函数可以接受一个或多个函数作为参数
- 函数可以作为另一个函数的结果返回
- 函数可以被修改
- 函数可以被赋值给变量

在本节中，我们将涵盖：

1. 将函数作为参数处理
2. 将函数作为返回值从其他函数返回
3. 使用 Python 闭包和装饰器

### 函数作为参数

```py
def sum_numbers(nums):  # 普通函数
    return sum(nums)    # 一个滥用内置 sum 函数的可怜函数 :<

def higher_order_function(f, lst):  # 函数作为参数
    summation = f(lst)
    return summation
result = higher_order_function(sum_numbers, [1, 2, 3, 4, 5])
print(result)       # 15
```

### 函数作为返回值

```py
def square(x):          # 平方函数
    return x ** 2

def cube(x):            # 立方函数
    return x ** 3

def absolute(x):        # 绝对值函数
    if x >= 0:
        return x
    else:
        return -(x)

def higher_order_function(type): # 返回函数的高阶函数
    if type == 'square':
        return square
    elif type == 'cube':
        return cube
    elif type == 'absolute':
        return absolute

result = higher_order_function('square')
print(result(3))       # 9
result = higher_order_function('cube')
print(result(3))       # 27
result = higher_order_function('absolute')
print(result(-3))      # 3
```

从上面的例子可以看出，高阶函数根据传入的参数返回不同的函数。

## Python 闭包（Closures）

Python 允许嵌套函数访问其封闭函数的外部作用域。这被称为闭包（Closure）。让我们看看闭包在 Python 中是如何工作的。在 Python 中，闭包是通过在一个封装函数内部嵌套一个函数，然后返回内部函数来创建的。请看下面的示例。

**示例（Example）：**

```py
def add_ten():
    ten = 10
    def add(num):
        return num + ten
    return add

closure_result = add_ten()
print(closure_result(5))  # 15
print(closure_result(10))  # 20
```

## Python 装饰器（Decorators）

装饰器（decorator）是 Python 中的一种设计模式，它允许用户在不修改现有对象结构的情况下为其添加新功能。装饰器通常在要装饰的函数定义之前调用。

### 创建装饰器

要创建装饰器函数，我们需要一个带有内部包装函数的外部函数。

**示例（Example）：**

```py
# 普通函数
def greeting():
    return 'Welcome to Python'
def uppercase_decorator(function):
    def wrapper():
        func = function()
        make_uppercase = func.upper()
        return make_uppercase
    return wrapper
g = uppercase_decorator(greeting)
print(g())          # WELCOME TO PYTHON

## 让我们用装饰器实现上面的示例

'''这个装饰器函数是一个高阶函数
它以函数作为参数'''
def uppercase_decorator(function):
    def wrapper():
        func = function()
        make_uppercase = func.upper()
        return make_uppercase
    return wrapper
@uppercase_decorator
def greeting():
    return 'Welcome to Python'
print(greeting())   # WELCOME TO PYTHON

```

### 将多个装饰器应用于单个函数

```py

'''这些装饰器函数是高阶函数
它们以函数作为参数'''

# 第一个装饰器
def uppercase_decorator(function):
    def wrapper():
        func = function()
        make_uppercase = func.upper()
        return make_uppercase
    return wrapper

# 第二个装饰器
def split_string_decorator(function):
    def wrapper():
        func = function()
        splitted_string = func.split()
        return splitted_string
    return wrapper

# 装饰器将从下到上执行
@split_string_decorator
@uppercase_decorator     # 在这种情况下装饰器的顺序很重要 - .upper() 函数不适用于列表
def greeting():
    return 'Welcome to Python'
print(greeting())   # ['WELCOME', 'TO', 'PYTHON']
```

### 在装饰器函数中接受参数

大多数时候我们需要函数接受参数，因此我们可能需要定义一个接受参数的装饰器。

```py
def decorator_with_parameters(function):
    def wrapper_accepting_parameters(para1, para2, para3):
        function(para1, para2, para3)
        print("I live in {}".format(para3))
    return wrapper_accepting_parameters

@decorator_with_parameters
def print_full_name(first_name, last_name, country):
    print("I am {} {}. I love to teach.".format(
        first_name, last_name))

print_full_name("Asabeneh", "Yetayeh",'Finland')
```

## 内置高阶函数

我们在本部分涵盖的一些内置高阶函数有 _map()_、_filter_ 和 _reduce_。
lambda 函数可以作为参数传递，lambda 函数的最佳用例是在 map、filter 和 reduce 等函数中。

### Python - Map 函数

map() 函数是一个内置函数，它接受一个函数和一个可迭代对象作为参数。

```py
    # 语法（syntax）
    map(function, iterable)
```

**示例 1：**

```py
numbers = [1, 2, 3, 4, 5] # 可迭代对象
def square(x):
    return x ** 2
numbers_squared = map(square, numbers)
print(list(numbers_squared))    # [1, 4, 9, 16, 25]
# 让我们用 lambda 函数来应用它
numbers_squared = map(lambda x : x ** 2, numbers)
print(list(numbers_squared))    # [1, 4, 9, 16, 25]
```

**示例 2：**

```py
numbers_str = ['1', '2', '3', '4', '5']  # 可迭代对象
numbers_int = map(int, numbers_str)
print(list(numbers_int))    # [1, 2, 3, 4, 5]
```

**示例 3：**

```py
names = ['Asabeneh', 'Lidiya', 'Ermias', 'Abraham']  # 可迭代对象

def change_to_upper(name):
    return name.upper()

names_upper_cased = map(change_to_upper, names)
print(list(names_upper_cased))    # ['ASABENEH', 'LIDIYA', 'ERMIAS', 'ABRAHAM']

# 让我们用 lambda 函数来应用它
names_upper_cased = map(lambda name: name.upper(), names)
print(list(names_upper_cased))    # ['ASABENEH', 'LIDIYA', 'ERMIAS', 'ABRAHAM']
```

map 实际做的是遍历列表。例如，它将名字转换为大写并返回一个新列表。

### Python - Filter 函数

filter() 函数调用指定的函数，该函数为指定可迭代对象（列表）的每个项返回布尔值。它过滤掉满足过滤条件的项。

```py
    # 语法（syntax）
    filter(function, iterable)
```

**示例 1：**

```py
# 让我们只过滤偶数
numbers = [1, 2, 3, 4, 5]  # 可迭代对象

def is_even(num):
    if num % 2 == 0:
        return True
    return False

even_numbers = filter(is_even, numbers)
print(list(even_numbers))       # [2, 4]
```

**示例 2：**

```py
numbers = [1, 2, 3, 4, 5]  # 可迭代对象

def is_odd(num):
    if num % 2 != 0:
        return True
    return False

odd_numbers = filter(is_odd, numbers)
print(list(odd_numbers))       # [1, 3, 5]
```

```py
# 过滤长名字
names = ['Asabeneh', 'Lidiya', 'Ermias', 'Abraham']  # 可迭代对象
def is_name_long(name):
    if len(name) > 7:
        return True
    return False

long_names = filter(is_name_long, names)
print(list(long_names))         # ['Asabeneh']
```

### Python - Reduce 函数

_reduce()_ 函数定义在 functools 模块中，我们应该从该模块导入它。像 map 和 filter 一样，它接受两个参数，一个函数和一个可迭代对象。然而，它不返回另一个可迭代对象，而是返回单个值。
**示例 1：**

```py
numbers_str = ['1', '2', '3', '4', '5']  # 可迭代对象
def add_two_nums(x, y):
    return int(x) + int(y)

total = reduce(add_two_nums, numbers_str)
print(total)    # 15
```

## 💻 练习：第 14 天

```py
countries = ['Estonia', 'Finland', 'Sweden', 'Denmark', 'Norway', 'Iceland']
names = ['Asabeneh', 'Lidiya', 'Ermias', 'Abraham']
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### 练习：第 1 级

1. 解释 map、filter 和 reduce 之间的区别。
2. 解释高阶函数、闭包和装饰器之间的区别。
3. 在 map、filter 或 reduce 之前定义一个调用函数，参见示例。
4. 使用 for 循环打印 countries 列表中的每个国家。
5. 使用 for 循环打印 names 列表中的每个名字。
6. 使用 for 循环打印 numbers 列表中的每个数字。

### 练习：第 2 级

1. 使用 map 将 countries 列表中的每个国家改为大写，创建一个新列表
1. 使用 map 将 numbers 列表中的每个数字改为它的平方，创建一个新列表
1. 使用 map 将 names 列表中的每个名字改为大写
1. 使用 filter 过滤掉包含 'land' 的国家。
1. 使用 filter 过滤掉恰好有六个字符的国家。
1. 使用 filter 过滤掉包含六个或更多字母的国家。
1. 使用 filter 过滤掉以 'E' 开头的国家
1. 链接两个或多个列表迭代器（例如 arr.map(callback).filter(callback).reduce(callback)）
1. 声明一个名为 get_string_lists 的函数，它接受一个列表作为参数，然后返回一个只包含字符串项的列表。
1. 使用 reduce 对 numbers 列表中的所有数字求和。
1. 使用 reduce 将所有国家连接起来，生成这个句子：Estonia, Finland, Sweden, Denmark, Norway, and Iceland are north European countries
1. 声明一个名为 categorize_countries 的函数，它返回具有某种共同模式的国家列表（你可以在本仓库中找到[counries 列表](https://github.com/Asabeneh/30-Days-Of-Python/blob/master/data/countries.py)，如 countries.js（例如 'land'、'ia'、'island'、'stan'））。
1. 创建一个返回字典的函数，其中键代表国家名称的首字母，值是以该字母开头的国家名称数量。
2. 声明一个 get_first_ten_countries 函数 - 它返回 data 文件夹中 countries.js 列表中的前十个国家。
1. 声明一个 get_last_ten_countries 函数，它返回 countries 列表中的最后十个国家。

### 练习：第 3 级

1. 使用 countries_data.py（https://github.com/Asabeneh/30-Days-Of-Python/blob/master/data/countries-data.py）文件并完成以下任务：
   - 按名称、首都、人口对国家进行排序
   - 按位置对使用最多的十种语言进行排序。
   - 对人口最多的十个国家进行排序。

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 13 天](../13_Day_List_comprehension_列表推导式/13_list_comprehension_列表推导式.md) | [第 15 天 >>](../15_Day_Python_type_errors_类型错误/15_python_type_errors_Python类型错误.md)
