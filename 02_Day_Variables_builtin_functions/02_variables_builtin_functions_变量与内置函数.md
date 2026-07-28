<div align="center">
  <h1> 🐍 30 Days Of Python：第 2 天 - 变量（Variables）、内置函数（Builtin Functions）</h1>
  <a class="header-badge" target="_blank" href="https://www.linkedin.com/in/asabeneh/">
  <img src="https://img.shields.io/badge/style--5eba00.svg?label=LinkedIn&logo=linkedin&style=social">
  </a>
  <a class="header-badge" target="_blank" href="https://twitter.com/Asabeneh">
  <img alt="Twitter Follow" src="https://img.shields.io/twitter/follow/asabeneh?style=social">
  </a>

<sub>作者（Author）：
<a href="https://www.linkedin.com/in/asabeneh/" target="_blank">Asabeneh Yetayeh</a><br>
<small> 第二版（Second Edition）：2021 年 7 月</small>
</sub>

</div>

[<< 第 1 天](../readme.md) | [第 3 天 >>](../03_Day_Operators/03_operators_运算符.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 2 天](#-第-2-天)
  - [内置函数（Built-in functions）](#内置函数built-in-functions)
  - [变量（Variables）](#变量variables)
    - [在一行中声明多个变量](#在一行中声明多个变量)
  - [数据类型（Data Types）](#数据类型data-types)
  - [检查数据类型与类型转换](#检查数据类型与类型转换)
  - [数字（Numbers）](#数字numbers)
  - [💻 练习 - 第 2 天](#-练习---第-2-天)
    - [练习：第 1 级](#练习第-1-级)
    - [练习：第 2 级](#练习第-2-级)

# 📘 第 2 天

## 内置函数（Built-in functions）

在 Python 中，我们有大量的内置函数（built-in function）。内置函数全局可用，也就是说你可以直接使用它们，而无需导入或配置。一些最常用的 Python 内置函数如下：_print()_、_len()_、_type()_、_int()_、_float()_、_str()_、_input()_、_list()_、_dict()_、_min()_、_max()_、_sum()_、_sorted()_、_open()_、_file()_、_help()_ 和 _dir()_。在下面的表格中，你将看到从 [Python 官方文档](https://docs.python.org/3/library/functions.html) 摘录的 Python 内置函数完整列表。

![Built-in Functions](../images/builtin-functions.png)

让我们打开 Python shell（交互式解释器），开始使用一些最常见的内置函数。

![Built-in functions](../images/builtin-functions_practice.png)

让我们通过使用不同的内置函数来进一步练习。

![Help and Dir Built in Functions](../images/help_and_dir_builtin.png)

正如你在上面的终端中所见，Python 拥有一些保留字（reserved words）。我们不会使用保留字来声明变量（variable）或函数（function）。我们将在下一节介绍变量。

我相信，到目前为止你已经对内置函数有所了解了。让我们再练习一次内置函数，然后继续进入下一节。

![Min Max Sum](../images/builtin-functional-final.png)

## 变量（Variables）

变量在计算机内存（memory）中存储数据。在许多编程语言中，推荐使用助记变量（mnemonic variable）。助记变量是指易于记忆和关联的变量名。变量指向存储数据的内存地址。

变量名开头不允许使用数字、特殊字符或连字符。变量可以有一个简短的名字（如 x、y、z），但强烈推荐使用更具描述性的名字（firstname、lastname、age、country）。

Python 变量命名规则

- 变量名必须以字母或下划线字符开头
- 变量名不能以数字开头
- 变量名只能包含字母数字字符和下划线（A-z、0-9 和 _）
- 变量名区分大小写（firstname、Firstname、FirstName 和 FIRSTNAME 是不同的变量）

以下是一些有效变量名的示例：

```shell
firstname
lastname
age
country
city
first_name
last_name
capital_city
_if # 如果我们想将保留字用作变量
year_2021
year2021
current_year_2021
birth_year
num1
num2
```

无效的变量名

```shell
first-name
first@name
first$name
num-1
1num
```

我们将使用已被许多 Python 开发者采用的 Python 标准变量命名风格。Python 开发者使用蛇形命名法（snake case，即 snake_case）作为变量命名约定。对于包含多个单词的变量，我们在每个单词后使用下划线字符（例如 first_name、last_name、engine_rotation_speed）。下面的示例是变量的标准命名方式，当变量名超过一个单词时需要使用下划线。

当我们为变量分配某种数据类型时，这称为变量声明（variable declaration）。例如在下面的示例中，我的名字被赋值给变量 first_name。等号是一个赋值运算符（assignment operator）。赋值意味着将数据存储在变量中。Python 中的等号并不像数学中表示相等。

_示例：_

```py
# Python 中的变量
first_name = 'Asabeneh'
last_name = 'Yetayeh'
country = 'Finland'
city = 'Helsinki'
age = 250
is_married = True
skills = ['HTML', 'CSS', 'JS', 'React', 'Python']
person_info = {
   'firstname':'Asabeneh',
   'lastname':'Yetayeh',
   'country':'Finland',
   'city':'Helsinki'
   }
```

让我们使用 _print()_ 和 _len()_ 内置函数。print 函数接受无限数量的参数（argument）。参数是我们可以传入或放在函数括号内的值，请看下面的示例。

**示例：**

```py
print('Hello, World!') # 文本 Hello, World! 是一个参数
print('Hello',',', 'World','!') # 它可以接受多个参数，这里传入了四个参数
print(len('Hello, World!')) # 它只接受一个参数
```

让我们打印并找出在顶部声明的变量的长度：

**示例：**

```py
# 打印存储在变量中的值

print('First name:', first_name)
print('First name length:', len(first_name))
print('Last name: ', last_name)
print('Last name length: ', len(last_name))
print('Country: ', country)
print('City: ', city)
print('Age: ', age)
print('Married: ', is_married)
print('Skills: ', skills)
print('Person information: ', person_info)
```

### 在一行中多个变量

多个变量也可以在一行中声明：

**示例：**

```py
first_name, last_name, country, age, is_married = 'Asabeneh', 'Yetayeh', 'Helsink', 250, True

print(first_name, last_name, country, age, is_married)
print('First name:', first_name)
print('Last name: ', last_name)
print('Country: ', country)
print('Age: ', age)
print('Married: ', is_married)
```

使用 _input()_ 内置函数获取用户输入（user input）。让我们将用户输入的数据赋值给 first_name 和 age 变量。
**示例：**

```py
first_name = input('What is your name: ')
age = input('How old are you? ')

print(first_name)
print(age)
```

## 数据类型（Data Types）

Python 中有多种数据类型（data type）。要识别数据类型，我们使用 _type_ 内置函数。我希望你专注于深入理解不同的数据类型。在编程中，一切都是关于数据类型的。我在一开始就介绍过数据类型，现在它再次出现，因为每个主题都与数据类型相关。我们将在各自的章节中更详细地介绍数据类型。

## 检查数据类型与类型转换

- 检查数据类型：要检查某些数据/变量的数据类型，我们使用 _type_
  **示例：**

```py
# 不同的 Python 数据类型
# 让我们声明具有各种数据类型的变量

first_name = 'Asabeneh'     # str
last_name = 'Yetayeh'       # str
country = 'Finland'         # str
city= 'Helsinki'            # str
age = 250                   # int，这不是我的真实年龄，不用担心

# 打印类型
print(type('Asabeneh'))          # str
print(type(first_name))          # str
print(type(10))                  # int
print(type(3.14))                # float
print(type(1 + 1j))              # complex
print(type(True))                # bool
print(type([1, 2, 3, 4]))        # list
print(type({'name':'Asabeneh'})) # dict
print(type((1,2)))               # tuple
print(type(zip([1,2],[3,4])))    # zip
```

- 类型转换（Casting）：将一种数据类型转换为另一种数据类型。我们使用 _int()_、_float()_、_str()_、_list_、_set_
  当我们进行算术运算时，字符串数字应首先转换为 int 或 float，否则将返回错误（error）。如果我们将数字与字符串拼接，数字应首先转换为字符串。我们将在字符串章节中讨论拼接。

  **示例：**

```py
# int 转 float
num_int = 10
print('num_int',num_int)         # 10
num_float = float(num_int)
print('num_float:', num_float)   # 10.0

# float 转 int
gravity = 9.81
print(int(gravity))             # 9

# int 转 str
num_int = 10
print(num_int)                  # 10
num_str = str(num_int)
print(num_str)                  # '10'

# str 转 int 或 float
num_str = '10.6'
num_float = float(num_str)  # 先将字符串转换为浮点数
num_int = int(num_float)    # 然后再将浮点数转换为整数
print('num_int', int(num_str))      # 10
print('num_float', float(num_str))  # 10.6
num_int = int(num_float)
print('num_int', int(num_int))      # 10

# str 转 list
first_name = 'Asabeneh'
print(first_name)               # 'Asabeneh'
first_name_to_list = list(first_name)
print(first_name_to_list)            # ['A', 's', 'a', 'b', 'e', 'n', 'e', 'h']
```

## 数字（Numbers）

Python 中的数字数据类型：

1. 整数（Integers）：整数（负数、零和正数）
   示例：
   ... -3, -2, -1, 0, 1, 2, 3 ...

2. 浮点数（Floating Point Numbers，小数）
   示例：
   ... -3.5, -2.25, -1.0, 0.0, 1.1, 2.2, 3.5 ...

3. 复数（Complex Numbers）
   示例：
   1 + j, 2 + 4j, 1 - 1j

🌕 你太棒了。你刚刚完成了第 2 天的挑战，在通往伟大的道路上已经领先了两步。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 2 天

### 练习：第 1 级

1. 在 30DaysOfPython 中创建一个名为 day_2 的文件夹。在此文件夹中创建一个名为 variables.py 的文件
2. 编写一条 Python 注释，内容为 'Day 2: 30 Days of python programming'
3. 声明一个名为 first name 的变量并为其赋值
4. 声明一个名为 last name 的变量并为其赋值
5. 声明一个名为 full name 的变量并为其赋值
6. 声明一个名为 country 的变量并为其赋值
7. 声明一个名为 city 的变量并为其赋值
8. 声明一个名为 age 的变量并为其赋值
9. 声明一个名为 year 的变量并为其赋值
10. 声明一个名为 is_married 的变量并为其赋值
11. 声明一个名为 is_true 的变量并为其赋值
12. 声明一个名为 is_light_on 的变量并为其赋值
13. 在一行中声明多个变量

### 练习：第 2 级

1. 使用 type() 内置函数检查所有变量的数据类型
2. 使用 _len()_ 内置函数，找出你的名字的长度
3. 比较你的名字和姓氏的长度
4. 将 5 声明为 num_one，将 4 声明为 num_two
5. 将 num_one 和 num_two 相加，并将值赋给一个名为 total 的变量
6. 用 num_one 减去 num_two，并将值赋给一个名为 diff 的变量
7. 将 num_two 和 num_one 相乘，并将值赋给一个名为 product 的变量
8. 用 num_one 除以 num_two，并将值赋给一个名为 division 的变量
9. 使用取模除法（modulus division）求 num_two 除以 num_one 的余数，并将值赋给一个名为 remainder 的变量
10. 计算 num_one 的 num_two 次幂，并将值赋给一个名为 exp 的变量
11. 求 num_one 除以 num_two 的整除结果（floor division），并将值赋给一个名为 floor_division 的变量
12. 一个圆的半径是 30 米。
    1. 计算圆的面积，并将值赋给名为 _area_of_circle_ 的变量
    2. 计算圆的周长，并将值赋给名为 _circum_of_circle_ 的变量
    3. 将半径作为用户输入，并计算面积
13. 使用内置的 input 函数获取用户的名字、姓氏、国家和年龄，并将值存储到相应的变量名中
14. 在 Python shell 或你的文件中运行 help('keywords') 来检查 Python 的保留字或关键字

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 1 天](../readme.md) | [第 3 天 >>](../03_Day_Operators/03_operators_运算符.md)
