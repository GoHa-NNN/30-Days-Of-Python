<div align="center">
  <h1> 🐍 30 Days Of Python：第 9 天 - 条件语句（Conditionals）</h1>
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

[<< 第 8 天](../08_Day_Dictionaries/08_dictionaries.md) | [第 10 天 >>](../10_Day_Loops/10_loops.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 9 天](#-第-9-天)
  - [条件语句（Conditionals）](#条件语句conditionals)
    - [If 条件](#if-条件)
    - [If Else](#if-else)
    - [If Elif Else](#if-elif-else)
    - [简写形式（Short Hand）](#简写形式short-hand)
    - [嵌套条件（Nested Conditions）](#嵌套条件nested-conditions)
    - [If 条件与逻辑运算符](#if-条件与逻辑运算符)
    - [If 与 Or 逻辑运算符](#if-与-or-逻辑运算符)
  - [💻 练习 - 第 9 天](#-练习---第-9-天)
    - [练习：第 1 级](#练习第-1-级)
    - [练习：第 2 级](#练习第-2-级)
    - [练习：第 3 级](#练习第-3-级)

# 📘 第 9 天

## 条件语句（Conditionals）

默认情况下，Python 脚本中的语句从上到下顺序执行。如果处理逻辑需要，可以通过两种方式改变顺序执行流程：

- 条件执行（Conditional execution）：如果某个表达式为真，则执行一条或多条语句的代码块
- 重复执行（Repetitive execution）：只要某个表达式为真，就重复执行一条或多条语句的代码块。在本节中，我们将介绍 _if_、_else_、_elif_ 语句。我们在前面章节学到的比较运算符和逻辑运算符在这里会很有用。

### If 条件

在 Python 和其他编程语言中，关键字 _if_ 用于检查条件是否为真并执行代码块（block code）。记住冒号后的缩进。

```py
# 语法
if condition:
    # 代码的这部分针对真值条件运行
```

**示例：1**

```py
a = 3
if a > 0:
    print('A is a positive number')
# A is a positive number
```

正如你在上面的示例中所见，3 大于 0。条件为真，代码块被执行了。然而，如果条件为假，我们就看不到结果。为了看到假值条件的结果，我们应该有另一个代码块，即 _else_。

### If Else

如果条件为真，第一个代码块将被执行；如果不是，则执行 else 条件。

```py
# 语法
if condition:
    # 代码的这部分针对真值条件运行
else:
    # 代码的这部分针对假值条件运行
```

**示例：**

```py
a = 3
if a < 0:
    print('A is a negative number')
else:
    print('A is a positive number')
```

上面的条件证明为假，因此 else 代码块被执行了。如果我们的条件超过两个怎么办？我们可以使用 _elif_。

### If Elif Else

在日常生活中，我们每天都在做决定。我们不是通过检查一两个条件来做决定，而是通过多个条件。与生活类似，编程也充满了条件。当我们有多个条件时使用 _elif_。

```py
# 语法
if condition:
    code
elif condition:
    code
else:
    code

```

**示例：**

```py
a = 0
if a > 0:
    print('A is a positive number')
elif a < 0:
    print('A is a negative number')
else:
    print('A is zero')
```

### 简写形式（Short Hand）

```py
# 语法
code if condition else code
```

**示例：**

```py
a = 3
print('A is positive') if a > 0 else print('A is negative') # 满足第一个条件，将打印 'A is positive'
```

### 嵌套条件（Nested Conditions）

条件可以嵌套

```py
# 语法
if condition:
    code
    if condition:
    code
```

**示例：**

```py
a = 0
if a > 0:
    if a % 2 == 0:
        print('A is a positive and even integer')
    else:
        print('A is a positive number')
elif a == 0:
    print('A is zero')
else:
    print('A is a negative number')

```

我们可以通过使用逻辑运算符 _and_ 来避免编写嵌套条件。

### If 条件与逻辑运算符

```py
# 语法
if condition and condition:
    code
```

**示例：**

```py
a = 0
if a > 0 and a % 2 == 0:
        print('A is an even and positive integer')
elif a > 0 and a % 2 !=  0:
     print('A is a positive integer')
elif a == 0:
    print('A is zero')
else:
    print('A is negative')
```

### If 与 Or 逻辑运算符

```py
# 语法
if condition or condition:
    code
```

**示例：**

```py
user = 'James'
access_level = 3
if user == 'admin' or access_level >= 4:
        print('Access granted!')
else:
    print('Access denied!')
```

🌕 你做得很棒。永远不要放弃，因为伟大的事情需要时间。你刚刚完成了第 9 天的挑战，在通往伟大的道路上已经领先了九步。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 9 天

### 练习：第 1 级

1. 使用 input("Enter your age: ") 获取用户输入。如果用户年满 18 岁或以上，给出反馈：You are old enough to drive。如果未满 18 岁，给出反馈说明还需要等多少年。输出：

    ```sh
    Enter your age: 30
    You are old enough to learn to drive.
    Output:
    Enter your age: 15
    You need 3 more years to learn to drive.
    ```

2. 使用 if … else 比较 my_age 和 your_age 的值。谁年龄更大（我还是你）？使用 input("Enter your age: ") 获取年龄作为输入。你可以使用嵌套条件，当年龄差为 1 年时打印 'year'，差距更大时打印 'years'，如果 my_age = your_age 则打印自定义文本。输出：

    ```sh
    Enter your age: 30
    You are 5 years older than me.
    ```

3. 使用 input prompt 从用户处获取两个数字。如果 a 大于 b，返回 a is greater than b；如果 a 小于 b，返回 a is smaller than b；否则返回 a is equal to b。输出：

```sh
Enter number one: 4
Enter number two: 3
4 is greater than 3
```

### 练习：第 2 级

   1. 编写一个根据学生分数给出成绩的代码：

    ```sh
    90-100, A
    80-89, B
    70-79, C
    60-69, D
    0-59, F
    ```

   2. 从用户输入获取月份，然后检查季节是 Autumn（秋季）、Winter（冬季）、Spring（春季）还是 Summer（夏季）。如果用户输入是：
    September、October 或 November，季节为 Autumn。
    December、January 或 February，季节为 Winter。
    March、April 或 May，季节为 Spring
    June、July 或 August，季节为 Summer
   3. 以下列表包含一些水果：

    ```sh
    fruits = ['banana', 'orange', 'mango', 'lemon']
    ```

    如果水果不存在于列表中，将该水果添加到列表中并打印修改后的列表。如果水果已存在，打印 'That fruit already exist in the list'

### 练习：第 3 级

   1. 这里有一个 person 字典。请随意修改它！

```py
        person={
    'first_name': 'Asabeneh',
    'last_name': 'Yetayeh',
    'age': 250,
    'country': 'Finland',
    'is_married': True,
    'skills': ['JavaScript', 'React', 'Node', 'MongoDB', 'Python'],
    'address': {
        'street': 'Space street',
        'zipcode': '02210'
    }
    }
```

     * 检查 person 字典是否有 skills 键，如果有，打印出 skills 列表中间的项。
     * 检查 person 字典是否有 skills 键，如果有，检查此人是否具有 'Python' 技能并打印结果。
     * 如果一个人的技能只有 JavaScript 和 React，打印 'He is a front end developer'；如果此人的技能有 Node、Python、MongoDB，打印 'He is a backend developer'；如果此人的技能有 React、Node 和 MongoDB，打印 'He is a fullstack developer'；否则打印 'unknown title' - 为了获得更准确的结果，可以嵌套更多条件！
     * 如果此人已婚且居住在芬兰，请按以下格式打印信息：

```py
    Asabeneh Yetayeh lives in Finland. He is married.
```

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 8 天](../08_Day_Dictionaries/08_dictionaries.md) | [第 10 天 >>](../10_Day_Loops/10_loops.md)
