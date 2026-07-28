<div align="center">
  <h1> 🐍 30 Days Of Python：第 3 天 - 运算符（Operators）</h1>
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

[<< 第 2 天](../02_Day_Variables_builtin_functions/02_variables_builtin_functions_变量与内置函数.md) | [第 4 天 >>](../04_Day_Strings/04_strings_字符串.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 3 天](#-第-3-天)
  - [布尔类型（Boolean）](#布尔类型boolean)
  - [运算符（Operators）](#运算符operators)
    - [赋值运算符（Assignment Operators）](#赋值运算符assignment-operators)
    - [算术运算符（Arithmetic Operators）](#算术运算符arithmetic-operators)
    - [比较运算符（Comparison Operators）](#比较运算符comparison-operators)
    - [逻辑运算符（Logical Operators）](#逻辑运算符logical-operators)
  - [💻 练习 - 第 3 天](#-练习---第-3-天)

# 📘 第 3 天

## 布尔类型（Boolean）

布尔（boolean）数据类型表示两个值之一：_True_ 或 _False_。一旦我们开始使用比较运算符（comparison operator），这些数据类型的作用就会清晰起来。与 JavaScript 不同，True 的首字母 **T** 和 False 的首字母 **F** 必须大写。
**示例：布尔值**

```py
print(True)
print(False)
```

## 运算符（Operators）

Python 语言支持多种类型的运算符。在本节中，我们将重点介绍其中几种。

### 赋值运算符（Assignment Operators）

赋值运算符用于为变量赋值。让我们以 = 为例。数学中的等号表示两个值相等，然而在 Python 中，它意味着我们将一个值存储在某个变量中，我们称之为赋值（assignment）或给变量赋值。下表展示了不同类型的 Python 赋值运算符，摘自 [w3school](https://www.w3schools.com/python/python_operators.asp)。

![Assignment Operators](../images/assignment_operators.png)

### 算术运算符（Arithmetic Operators）

- 加法（Addition，+）：a + b
- 减法（Subtraction，-）：a - b
- 乘法（Multiplication，*）：a * b
- 除法（Division，/）：a / b
- 取模（Modulus，%）：a % b
- 整除（Floor division，//）：a // b
- 幂运算（Exponentiation，**）：a ** b

![Arithmetic Operators](../images/arithmetic_operators.png)

**示例：整数（Integers）**

```py
# Python 中的算术运算
# 整数

print('Addition: ', 1 + 2)        # 3
print('Subtraction: ', 2 - 1)     # 1
print('Multiplication: ', 2 * 3)  # 6
print ('Division: ', 4 / 2)       # 2.0  Python 中的除法会得到浮点数
print('Division: ', 6 / 2)        # 3.0
print('Division: ', 7 / 2)        # 3.5
print('Division without the remainder: ', 7 // 2)   # 3, 不带浮点数或余数的结果
print ('Division without the remainder: ',7 // 3)   # 2
print('Modulus: ', 3 % 2)         # 1, 给出余数
print('Exponentiation: ', 2 ** 3) # 8 表示 2 * 2 * 2
```

**示例：浮点数（Floats）**

```py
# 浮点数
print('Floating Point Number, PI', 3.14)
print('Floating Point Number, gravity', 9.81)
```

**示例：复数（Complex numbers）**

```py
# 复数
print('Complex number: ', 1 + 1j)
print('Multiplying complex numbers: ',(1 + 1j) * (1 - 1j))
```

让我们声明一个变量并为其赋值数字数据类型。我将使用单字符变量，但请记住不要养成声明此类变量的习惯。变量名应该始终是助记的。

**示例：**

```python
# 首先在顶部声明变量

a = 3 # a 是变量名，3 是整数数据类型
b = 2 # b 是变量名，2 是整数数据类型

# 算术运算并将结果赋值给变量
total = a + b
diff = a - b
product = a * b
division = a / b
remainder = a % b
floor_division = a // b
exponential = a ** b

# 我本应该用 sum 而不是 total，但 sum 是内置函数 - 尽量避免覆盖内置函数
print(total) # 如果你不在 print 中标注一些字符串，你永远不知道结果从哪里来
print('a + b = ', total)
print('a - b = ', diff)
print('a * b = ', product)
print('a / b = ', division)
print('a % b = ', remainder)
print('a // b = ', floor_division)
print('a ** b = ', exponential)
```

**示例：**

```py
print('== Addition, Subtraction, Multiplication, Division, Modulus ==')

# 声明值并将它们组织在一起
num_one = 3
num_two = 4

# 算术运算
total = num_one + num_two
diff = num_two - num_one
product = num_one * num_two
div = num_two / num_one
remainder = num_two % num_one

# 带标签打印值
print('total: ', total)
print('difference: ', diff)
print('product: ', product)
print('division: ', div)
print('remainder: ', remainder)
```

让我们开始将知识点串联起来，利用我们已经知道的内容来计算（面积、体积、密度、重量、周长、距离、力）。

**示例：**

```py
# 计算圆的面积
radius = 10                                 # 圆的半径
area_of_circle = 3.14 * radius ** 2         # 两个 * 号表示指数或幂
print('Area of a circle:', area_of_circle)

# 计算矩形的面积
length = 10
width = 20
area_of_rectangle = length * width
print('Area of rectangle:', area_of_rectangle)

# 计算物体的重量
mass = 75
gravity = 9.81
weight = mass * gravity
print(weight, 'N')                         # 为重量添加单位

# 计算液体的密度
mass = 75 # 单位：Kg
volume = 0.075 # 单位：立方米
density = mass / volume # 1000 Kg/m^3
print(density, 'Kg/m^3') # 为密度添加单位

```

### 比较运算符（Comparison Operators）

在编程中，我们会比较值，使用比较运算符来比较两个值。我们检查一个值是否大于、小于或等于另一个值。下表展示了 Python 比较运算符，摘自 [w3school](https://www.w3schools.com/python/python_operators.asp)。

![Comparison Operators](../images/comparison_operators.png)
**示例：比较运算符**

```py
print(3 > 2)     # True，因为 3 大于 2
print(3 >= 2)    # True，因为 3 大于 2
print(3 < 2)     # False，因为 3 大于 2
print(2 < 3)     # True，因为 2 小于 3
print(2 <= 3)    # True，因为 2 小于 3
print(3 == 2)    # False，因为 3 不等于 2
print(3 != 2)    # True，因为 3 不等于 2
print(len('mango') == len('avocado'))  # False
print(len('mango') != len('avocado'))  # True
print(len('mango') < len('avocado'))   # True
print(len('milk') != len('meat'))      # False
print(len('milk') == len('meat'))      # True
print(len('tomato') == len('potato'))  # True
print(len('python') > len('dragon'))   # False


# 比较的结果要么是 True，要么是 False

print('True == True: ', True == True)
print('True == False: ', True == False)
print('False == False:', False == False)
```

除了上述比较运算符，Python 还使用：

- _is_: 如果两个变量是同一个对象，则返回 true（x is y）
- _is not_: 如果两个变量不是同一个对象，则返回 true（x is not y）
- _in_: 如果查询的列表包含某个项目，则返回 True（x in y）
- _not in_: 如果查询的列表不包含某个项目，则返回 True（x not in y）

```py
print('1 is 1', 1 is 1)                   # True - 因为数据值相同
print('1 is not 2', 1 is not 2)           # True - 因为 1 不等于 2
print('A in Asabeneh', 'A' in 'Asabeneh') # True - A 在字符串中被找到
print('B not in Asabeneh', 'B' in 'Asabeneh') # False - 没有大写 B
print('coding' in 'coding for all') # True - 因为 coding for all 包含 coding 这个词
print('a in an:', 'a' in 'an')      # True
print('4 is 2 ** 2:', 4 is 2 ** 2)   # True
```

### 逻辑运算符（Logical Operators）

与其他编程语言不同，Python 使用关键字 _and_、_or_ 和 _not_ 作为逻辑运算符。逻辑运算符用于组合条件语句：

![Logical Operators](../images/logical_operators.png)

```py
print(3 > 2 and 4 > 3) # True - 因为两个语句都为真
print(3 > 2 and 4 < 3) # False - 因为第二个语句为假
print(3 < 2 and 4 < 3) # False - 因为两个语句都为假
print('True and True: ', True and True)
print(3 > 2 or 4 > 3)  # True - 因为两个语句都为真
print(3 > 2 or 4 < 3)  # True - 因为其中一个语句为真
print(3 < 2 or 4 < 3)  # False - 因为两个语句都为假
print('True or False:', True or False)
print(not 3 > 2)     # False - 因为 3 > 2 为真，not True 则为 False
print(not True)      # False - 取反，not 运算符将真变为假
print(not False)     # True
print(not not True)  # True
print(not not False) # False

```

🌕 你拥有无限的能量。你刚刚完成了第 3 天的挑战，在通往伟大的道路上已经领先了三步。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 3 天

1. 将你的年龄声明为整数变量
2. 将你的身高声明为浮点数变量
3. 声明一个存储复数的变量
4. 编写一个脚本，提示用户输入三角形的底和高，并计算该三角形的面积（面积 = 0.5 x 底 x 高）。

```py
    Enter base: 20
    Enter height: 10
    The area of the triangle is 100
```

5. 编写一个脚本，提示用户输入三角形的边 a、边 b 和边 c。计算三角形的周长（周长 = a + b + c）。

```py
Enter side a: 5
Enter side b: 4
Enter side c: 3
The perimeter of the triangle is 12
```

6. 使用 prompt 获取长方形的长和宽。计算其面积（面积 = 长 x 宽）和周长（周长 = 2 x (长 + 宽)）
7. 使用 prompt 获取圆的半径。计算面积（面积 = pi x r x r）和周长（c = 2 x pi x r），其中 pi = 3.14
8. 计算 y = 2x - 2 的斜率、x 截距和 y 截距
9. 斜率是（m = y2-y1/x2-x1）。求点 (2, 2) 和点 (6, 10) 之间的斜率和[欧几里得距离](https://en.wikipedia.org/wiki/Euclidean_distance#:~:text=In%20mathematics%2C%20the%20Euclidean%20distance,being%20called%20the%20Pythagorean%20distance.)
10. 比较第 8 题和第 9 题的斜率
11. 计算 y 的值（y = x^2 + 6x + 9）。尝试使用不同的 x 值，找出当 y 为 0 时的 x 值
12. 求 'python' 和 'dragon' 的长度，并编写一个为假的比较语句
13. 使用 _and_ 运算符检查 'on' 是否同时存在于 'python' 和 'dragon' 中
14. _I hope this course is not full of jargon_。使用 _in_ 运算符检查 _jargon_ 是否在句子中
15. 'dragon' 和 'python' 中都不存在 'on'
16. 求文本 _python_ 的长度，并将值转换为浮点数，再转换为字符串
17. 偶数能被 2 整除且余数为零。如何使用 Python 检查一个数是否为偶数？
18. 检查 7 除以 3 的整除结果是否等于 2.7 转换为 int 后的值
19. 检查 '10' 的类型是否等于 10 的类型
20. 检查 int('9.8') 是否等于 10
21. 编写一个脚本，提示用户输入工作小时数和每小时报酬。计算该人的工资？

```py
Enter hours: 40
Enter rate per hour: 28
Your weekly earning is 1120
```

22. 编写一个脚本，提示用户输入已生活的年数。计算一个人能生活的秒数。假设一个人可以活一百年

```py
Enter number of years you have lived: 100
You have lived for 3153600000 seconds.
```

23. 编写一个 Python 脚本，显示以下表格

```py
1 1 1 1 1
2 1 2 4 8
3 1 3 9 27
4 1 4 16 64
5 1 5 25 125
```

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 2 天](../02_Day_Variables_builtin_functions/02_variables_builtin_functions_变量与内置函数.md) | [第 4 天 >>](../04_Day_Strings/04_strings_字符串.md)
