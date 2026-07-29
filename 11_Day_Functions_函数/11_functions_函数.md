<div align="center">
  <h1> 🐍 30 Days Of Python：第 11 天 - 函数（Functions）</h1>
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

[<< 第 10 天](../10_Day_Loops_循环/10_loops_循环.md) | [第 12 天 >>](../12_Day_Modules_模块/12_modules_模块.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 11 天](#-第-11-天)
  - [函数（Functions）](#函数functions)
    - [定义函数](#定义函数)
    - [声明和调用函数](#声明和调用函数)
    - [无参数的函数](#无参数的函数)
    - [返回值的函数 - 第 1 部分](#返回值的函数---第-1-部分)
    - [带参数的函数](#带参数的函数)
    - [使用键和值传递参数](#使用键和值传递参数)
    - [返回值的函数 - 第 2 部分](#返回值的函数---第-2-部分)
    - [带默认参数的函数](#带默认参数的函数)
    - [任意数量的参数](#任意数量的参数)
    - [函数中的默认参数和任意数量参数](#函数中的默认参数和任意数量参数)
    - [函数作为另一个函数的参数](#函数作为另一个函数的参数)
  - [感言（Testimony）](#感言testimony)
  - [💻 练习：第 11 天](#-练习第-11-天)
    - [练习：第 1 级](#练习第-1-级)
    - [练习：第 2 级](#练习第-2-级)
    - [练习：第 3 级](#练习第-3-级)

# 📘 第 11 天

## 函数（Functions）

到目前为止，我们已经见过许多 Python 内置函数（built-in function）。在本节（section）中，我们将重点关注自定义函数。什么是函数？在开始编写函数之前，让我们先了解一下什么是函数以及为什么需要它们。

### 定义函数

函数（function）是一段可重复使用的代码块（block of code）或编程语句（programming statements），用于执行特定任务。要定义（define）或声明（declare）一个函数，Python 提供了 _def_ 关键字。以下是定义函数的语法（syntax）。函数代码块只有在函数被调用（call）或执行（invoke）时才会运行。

### 声明和调用函数

当我们创建一个函数时，我们称之为声明（declare）一个函数。当我们开始使用它时，我们称之为调用（call）或执行（invoke）一个函数。函数可以在有参数（parameter）或无参数的情况下声明。

```py
# 语法（syntax）
# 声明一个函数
def function_name():
    codes
    codes
# 调用函数
function_name()
```

### 无参数的函数

函数可以在没有参数的情况下声明。

**示例（Example）：**

```py
def generate_full_name ():
    first_name = 'Asabeneh'
    last_name = 'Yetayeh'
    space = ' '
    full_name = first_name + space + last_name
    print(full_name)
generate_full_name () # 调用函数

def add_two_numbers ():
    num_one = 2
    num_two = 3
    total = num_one + num_two
    print(total)
add_two_numbers()
```

### 返回值的函数 - 第 1 部分

函数使用 _return_ 语句返回值。如果一个函数没有 return 语句，它会返回 None。让我们使用 return 重写上面的函数。从现在开始，我们在调用函数并打印时从函数获取值。

```py
def generate_full_name ():
    first_name = 'Asabeneh'
    last_name = 'Yetayeh'
    space = ' '
    full_name = first_name + space + last_name
    return full_name
print(generate_full_name())

def add_two_numbers ():
    num_one = 2
    num_two = 3
    total = num_one + num_two
    return total
print(add_two_numbers())
```

### 带参数的函数

在函数中，我们可以将不同的数据类型（number、string、boolean、list、tuple、dictionary 或 set）作为参数传递。

- 单个参数：如果我们的函数接受一个参数，我们应该在调用函数时传入一个实参（argument）

```py
  # 语法（syntax）
  # 声明一个函数
  def function_name(parameter):
    codes
    codes
  # 调用函数
  print(function_name(argument))
```

**示例（Example）：**

```py
def greetings (name):
    message = name + ', welcome to Python for Everyone!'
    return message

print(greetings('Asabeneh'))

def add_ten(num):
    ten = 10
    return num + ten
print(add_ten(90))

def square_number(x):
    return x * x
print(square_number(2))

def area_of_circle (r):
    PI = 3.14
    area = PI * r ** 2
    return area
print(area_of_circle(10))

def sum_of_numbers(n):
    total = 0
    for i in range(n+1):
        total+=i
    return total
print(sum_of_numbers(10)) # 55
print(sum_of_numbers(100)) # 5050
```

- 两个参数：函数可能有也可能没有参数。函数也可以有两个或更多参数。如果我们的函数接受参数，我们应该在调用时传入实参。让我们看看一个带有两个参数的函数：

```py
  # 语法（syntax）
  # 声明一个函数
  def function_name(para1, para2):
    codes
    codes
  # 调用函数
  print(function_name(arg1, arg2))
```

**示例（Example）：**

```py
def generate_full_name (first_name, last_name):
    space = ' '
      full_name = first_name + space + last_name
      return full_name
print('Full Name: ', generate_full_name('Asabeneh','Yetayeh'))

def sum_two_numbers (num_one, num_two):
    sum = num_one + num_two
    return sum
print('Sum of two numbers: ', sum_two_numbers(1, 9))

def calculate_age (current_year, birth_year):
    age = current_year - birth_year
    return age

print('Age: ', calculate_age(2021, 1819))

def weight_of_object (mass, gravity):
    weight = str(mass * gravity)+ ' N' # 值必须先转换为字符串
    return weight
print('Weight of an object in Newtons: ', weight_of_object(100, 9.81))
```

### 使用键和值传递参数

如果我们使用键（key）和值（value）传递参数，参数的顺序无关紧要。

```py
# 语法（syntax）
# 声明一个函数
def function_name(para1, para2):
    codes
    codes
# 调用函数
print(function_name(para1 = 'John', para2 = 'Doe')) # 这里参数的顺序无关紧要
```

**示例（Example）：**

```py
def print_fullname(firstname, lastname):
    space = ' '
    full_name = firstname  + space + lastname
    print(full_name)
print_fullname(firstname = 'Asabeneh', lastname = 'Yetayeh')

def add_two_numbers (num1, num2):
    total = num1 + num2
    return total
print(add_two_numbers(num2 = 3, num1 = 2)) # 顺序无关紧要
```

### 返回值的函数 - 第 2 部分

如果我们没有用函数返回值，那么我们的函数默认返回 _None_。要用函数返回值，我们使用关键字 _return_ 后跟我们要返回的变量。我们可以从函数返回任何数据类型。

- 返回字符串：
**示例（Example）：**

```py
def print_name(firstname):
    return firstname
print_name('Asabeneh') # Asabeneh

def print_full_name(firstname, lastname):
    space = ' '
    full_name = firstname  + space + lastname
    return full_name
print_full_name(firstname='Asabeneh', lastname='Yetayeh')
```

- 返回数字：

**示例（Example）：**

```py
def add_two_numbers (num1, num2):
    total = num1 + num2
    return total
print(add_two_numbers(2, 3))

def calculate_age (current_year, birth_year):
    age = current_year - birth_year
    return age
print('Age: ', calculate_age(2019, 1819))
```

- 返回布尔值：
  **示例（Example）：**

```py
def is_even (n):
    if n % 2 == 0:
        return True    # return 会停止函数的进一步执行，类似于 break
    return False
print(is_even(10)) # True
print(is_even(7)) # False
```

- 返回列表：
  **示例（Example）：**

```py
def find_even_numbers(n):
    evens = []
    for i in range(n + 1):
        if i % 2 == 0:
            evens.append(i)
    return evens
print(find_even_numbers(10))
```

### 带默认参数的函数

有时我们在调用函数时为参数传递默认值。如果在调用函数时没有传递参数，将使用它们的默认值。

```py
# 语法（syntax）
# 声明一个函数
def function_name(param = value):
    codes
    codes
# 调用函数
function_name()
function_name(arg)
```

**示例（Example）：**

```py
def greetings (name = 'Peter'):
    message = name + ', welcome to Python for Everyone!'
    return message
print(greetings())
print(greetings('Asabeneh'))

def generate_full_name (first_name = 'Asabeneh', last_name = 'Yetayeh'):
    space = ' '
    full_name = first_name + space + last_name
    return full_name

print(generate_full_name())
print(generate_full_name('David','Smith'))

def calculate_age (birth_year,current_year = 2021):
    age = current_year - birth_year
    return age
print('Age: ', calculate_age(1821))

def weight_of_object (mass, gravity = 9.81):
    weight = str(mass * gravity)+ ' N' # 值必须先转换为字符串
    return weight
print('Weight of an object in Newtons: ', weight_of_object(100)) # 9.81 - 地球表面的平均重力
print('Weight of an object in Newtons: ', weight_of_object(100, 1.62)) # 月球表面的重力
```

### 任意数量的参数

如果我们不知道传递给函数的参数数量，可以通过在参数名前添加 \* 来创建一个接受任意数量参数的函数。

```py
# 语法（syntax）
# 声明一个函数
def function_name(*args):
    codes
    codes
# 调用函数
function_name(param1, param2, param3,..)
```

**示例（Example）：**

```py
def sum_all_nums(*nums):
    total = 0
    for num in nums:
        total += num     # 等同于 total = total + num
    return total
print(sum_all_nums(2, 3, 5)) # 10
```

### 函数中的默认参数和任意数量参数

```py
def generate_groups (team,*args):
    print(team)
    for i in args:
        print(i)
generate_groups('Team-1','Asabeneh','Brook','David','Eyob')
```

### 字典解包（Dictionary unpacking）

你可以使用一个键名匹配的字典来调用具有命名参数的函数。你可以使用 ``**`` 来实现。

```py
# 定义一个接受两个参数 'name' 和 'location' 的函数
def greet(name, location):
    # 使用提供的实参打印问候消息
    print("Hi there", name, "how is the weather in", location)

# 使用关键字参数调用函数
greet(name="Alice", location="New York")
# 输出：Hi there Alice how is the weather in New York

# 创建一个键与函数参数名匹配的字典
my_dict = {"name": "Alice", "location": "New York"}

# 使用字典解包调用函数
greet(**my_dict)
# ** 操作符将字典解包，将其键值对作为关键字参数传递给函数。
# 输出：Hi there Alice how is the weather in New York
```

### 任意数量的命名参数

你还可以定义一个函数来接受任意数量的命名参数。

```py
def arbitrary_named_args(**args):
    print("I received an arbitrary number of arguments, totaling", len(args))
    print("They are provided as a dictionary in my function:", type(args))
    print("Let's print them:")
    for k, v in args.items():
        print(" * key:", k, "value:", v)
```

除非必要，通常应避免这样做，因为它会使函数接受的内容和做的事情更难理解。

### 函数作为另一个函数的参数

```py
# 你可以将函数作为参数传递
def square_number (n):
    return n ** n
def do_something(f, x):
    return f(x)
print(do_something(square_number, 3)) # 27
```

🌕 到目前为止你已经取得了很大进步。继续加油！你刚刚完成了第 11 天的挑战，在通往伟大的道路上已经领先了 11 步。现在为你的大脑和肌肉做一些练习吧。

## 感言（Testimony）

现在是时候表达你对作者和 30DaysOfPython 的想法了。你可以在这个[链接](https://testimonial-s3sw.onrender.com/)上留下你的感言。

## 💻 练习：第 11 天

### 练习：第 1 级

1. 声明（Declare）一个名为 _add_two_numbers_ 的函数。它接受两个参数并返回它们的和。
2. 圆的面积计算方式如下：area = π x r x r。编写一个计算 _area_of_circle_ 的函数。
3. 编写一个名为 add_all_nums 的函数，它接受任意数量的参数并对所有参数求和。检查所有列表项是否都是数字类型。如果不是，给出合理的反馈。
4. 摄氏温度（°C）可以使用以下公式转换为华氏温度（°F）：°F = (°C x 9/5) + 32。编写一个将 °C 转换为 °F 的函数，_convert_celsius_to-fahrenheit_。
5. 编写一个名为 check-season 的函数，它接受一个月份参数并返回季节：Autumn、Winter、Spring 或 Summer。
6. 编写一个名为 calculate_slope 的函数，它返回线性方程的斜率。
7. 二次方程计算方式如下：ax² + bx + c = 0。编写一个计算二次方程解集的函数，_solve_quadratic_eqn_。
8. 声明一个名为 print_list 的函数。它接受一个列表作为参数并打印出列表的每个元素。
9. 声明一个名为 reverse_list 的函数。它接受一个数组作为参数并返回该数组的反转（使用循环）。

```py
print(reverse_list([1, 2, 3, 4, 5]))
# [5, 4, 3, 2, 1]
print(reverse_list(["A", "B", "C"]))
# ["C", "B", "A"]
```

10. 声明一个名为 capitalize_list_items 的函数。它接受一个列表作为参数并返回一个首字母大写的列表项
11. 声明一个名为 add_item 的函数。它接受一个列表和一个 item 参数。它返回一个在末尾添加了该项的列表。

```py
food_stuff = ['Potato', 'Tomato', 'Mango', 'Milk'];
print(add_item(food_stuff, 'Meat'))     # ['Potato', 'Tomato', 'Mango', 'Milk','Meat'];
numbers = [2, 3, 7, 9];
print(add_item(numbers, 5))      # [2, 3, 7, 9, 5]

```

12. 声明一个名为 remove_item 的函数。它接受一个列表和一个 item 参数。它返回一个移除了该项的列表。

```py
food_stuff = ['Potato', 'Tomato', 'Mango', 'Milk']
print(remove_item(food_stuff, 'Mango'))  # ['Potato', 'Tomato', 'Milk'];
numbers = [2, 3, 7, 9]
print(remove_item(numbers, 3))  # [2, 7, 9]
```

13. 声明一个名为 sum_of_numbers 的函数。它接受一个数字参数并添加该范围内的所有数字。

```py
print(sum_of_numbers(5))  # 15
print(sum_of_numbers(10)) # 55
print(sum_of_numbers(100)) # 5050
```

14. 声明一个名为 sum_of_odds 的函数。它接受一个数字参数并添加该范围内的所有奇数。
15. 声明一个名为 sum_of_even 的函数。它接受一个数字参数并添加该范围内的所有偶数。

### 练习：第 2 级

1. 声明一个名为 evens_and_odds 的函数。它接受一个正整数作为参数，并计算该数字中偶数和奇数的个数。

```py
    print(evens_and_odds(100))
    # The number of odds are 50.
    # The number of evens are 51.
```

1. 调用你的函数 factorial，它接受一个整数作为参数并返回该数字的阶乘
1. 调用你的函数 _is_empty_，它接受一个参数并检查它是否为空
1. 编写不同的函数，它们接受列表。它们应该 calculate_mean、calculate_median、calculate_mode、calculate_range、calculate_variance、calculate_std（标准差）。
1. 编写一个名为 _greet_ 的函数，它接受一个默认参数 _name_。如果没有提供参数，它应该打印 "Hello, Guest!"，否则应该按名字问候这个人。

```py
    greet()
    # "Hello, Guest!
    greet("Alice")
    # "Hello, Alice!"
```

1. 创建一个名为 _show_args_ 的函数，它接受任意数量的命名参数并打印它们的名称和值。
   ```py
   show_args(name="Alice", age=30, city="New York")
   # Received: name: Alice, age: 30, city: New York
   show_args(name="Bob", pet="Fluffy, the bunny")
   # Received: name: Bob, pet: Fluffy, the bunny
   ```


### 练习：第 3 级

1. 编写一个名为 is_prime 的函数，它检查一个数字是否为质数。
1. 编写一个函数，检查列表中的所有项是否都是唯一的。
1. 编写一个函数，检查列表中的所有项是否都是相同的数据类型。
1. 编写一个函数，检查提供的变量是否是有效的 Python 变量
1. 转到 data 文件夹并访问 countries-data.py 文件。

- 创建一个名为 the most_spoken_languages 的函数。它应该返回世界上使用最多的 10 种或 20 种语言，按降序排列
- 创建一个名为 the most_populated_countries 的函数。它应该返回世界上人口最多的 10 个或 20 个国家，按降序排列。

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 10 天](../10_Day_Loops_循环/10_loops_循环.md) | [第 12 天 >>](../12_Day_Modules_模块/12_modules_模块.md)
