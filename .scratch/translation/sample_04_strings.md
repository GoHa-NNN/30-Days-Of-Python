<div align="center">
  <h1> 🐍 30 Days Of Python：第 4 天 - 字符串（Strings）</h1>
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

[<< 第 3 天](../03_Day_Operators/03_operators.md) | [第 5 天 >>](../05_Day_Lists/05_lists.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [第 4 天](#第-4-天)
  - [字符串（Strings）](#字符串strings)
    - [创建字符串](#创建字符串)
    - [字符串拼接](#字符串拼接)
    - [字符串中的转义序列](#字符串中的转义序列)
    - [字符串格式化](#字符串格式化)
      - [旧式字符串格式化（% 操作符）](#旧式字符串格式化-操作符)
      - [新式字符串格式化（str.format）](#新式字符串格式化strformat)
      - [字符串插值 / f-string（Python 3.6+）](#字符串插值--f-stringpython-36)
    - [Python 字符串作为字符序列](#python-字符串作为字符序列)
      - [解包字符](#解包字符)
      - [通过索引访问字符串中的字符](#通过索引访问字符串中的字符)
      - [对 Python 字符串切片](#对-python-字符串切片)
      - [反转字符串](#反转字符串)
      - [切片时跳过字符](#切片时跳过字符)
    - [字符串方法](#字符串方法)
  - [💻 练习 - 第 4 天](#-练习---第-4-天)

# 第 4 天

## 字符串（Strings）

文本（Text）属于字符串（string）数据类型。任何以文本形式书写的数据都是字符串。任何被单引号、双引号或三引号包围的内容都是字符串。Python 提供了多种字符串方法（method）和内置函数（built-in function）来处理字符串数据类型。要检查字符串的长度，可以使用 len() 方法。

### 创建字符串

```py
letter = 'P'                # 字符串可以是一个单个字符，也可以是一堆文本
print(letter)               # P
print(len(letter))          # 1
greeting = 'Hello, World!'  # 字符串可以用单引号或双引号创建，"Hello, World!"
print(greeting)             # Hello, World!
print(len(greeting))        # 13
sentence = "I hope you are enjoying 30 days of Python Challenge"
print(sentence)
```

多行字符串（multiline string）通过使用三单引号（'''）或三双引号（"""）来创建。请看下面的示例。

```py
multiline_string = '''I am a teacher and enjoy teaching.
I didn't find anything as rewarding as empowering people.
That is why I created 30 days of python.'''
print(multiline_string)

# 另一种实现同样效果的方法
multiline_string = """I am a teacher and enjoy teaching.
I didn't find anything as rewarding as empowering people.
That is why I created 30 days of python."""
print(multiline_string)
```

### 字符串拼接

我们可以将字符串连接在一起。合并或连接字符串称为拼接（concatenation）。请看下面的示例：

```py
first_name = 'Asabeneh'
last_name = 'Yetayeh'
space = ' '
full_name = first_name  +  space + last_name
print(full_name) # Asabeneh Yetayeh
# 使用 len() 内置函数检查字符串的长度
print(len(first_name))  # 8
print(len(last_name))   # 7
print(len(first_name) > len(last_name)) # True
print(len(full_name)) # 16
```

### 字符串中的转义序列

在 Python 和其他编程语言中，反斜杠（\）后跟一个字符构成一个转义序列（escape sequence）。让我们看看最常见的转义字符：

- \n: 换行（new line）
- \t: 制表符（Tab），即 8 个空格
- \\\\: 反斜杠（Back slash）
- \\': 单引号（'）
- \\": 双引号（"）

现在，让我们通过示例看看上述转义序列的用法。

```py
print('I hope everyone is enjoying the Python Challenge.\nAre you ?') # 换行（line break）
print('Days\tTopics\tExercises') # 添加 tab 空格，即 4 个空格
print('Day 1\t5\t5')
print('Day 2\t6\t20')
print('Day 3\t5\t23')
print('Day 4\t1\t35')
print('This is a backslash  symbol (\\)') # 写入一个反斜杠
print('In every programming language it starts with \"Hello, World!\"') # 在单引号内写入双引号

# 输出（output）
I hope every one is enjoying the Python Challenge.
Are you ?
Days  Topics  Exercises
Day 1	5	    5
Day 2	6	    20
Day 3	5	    23
Day 4	1	    35
This is a backslash  symbol (\)
In every programming language it starts with "Hello, World!"
```

### 字符串格式化

#### 旧式字符串格式化（% 操作符）

在 Python 中，格式化字符串的方法有很多种。在本节（section）中，我们将介绍其中一部分。
"%" 操作符（operator）用于格式化一组被包在"元组（tuple）"（一种固定大小的列表）中的变量，配合格式化字符串（format string）一起使用，格式化字符串包含普通文本以及"参数说明符（argument specifier）"——例如 "%s"、"%d"、"%f"、"%.<small>数字位数</small>f" 这样的特殊符号。

- %s - 字符串（String）（或任何具有字符串表示的对象，如数字）
- %d - 整数（Integers）
- %f - 浮点数（Floating point numbers）
- "%.<small>数字位数</small>f" - 固定精度的浮点数

```py
# 纯字符串
first_name = 'Asabeneh'
last_name = 'Yetayeh'
language = 'Python'
formated_string = 'I am %s %s. I teach %s' %(first_name, last_name, language)
print(formated_string)

# 字符串与数字
radius = 10
pi = 3.14
area = pi * radius ** 2
formated_string = 'The area of circle with a radius %d is %.2f.' %(radius, area) # 2 表示小数点后保留 2 位有效数字

python_libraries = ['Django', 'Flask', 'NumPy', 'Matplotlib','Pandas']
formated_string = 'The following are python libraries:%s' % (python_libraries)
print(formated_string) # "The following are python libraries:['Django', 'Flask', 'NumPy', 'Matplotlib','Pandas']"
```

#### 新式字符串格式化（str.format）

这种格式化方式在 Python 3 中引入。

```py

first_name = 'Asabeneh'
last_name = 'Yetayeh'
language = 'Python'
formated_string = 'I am {} {}. I teach {}'.format(first_name, last_name, language)
print(formated_string)
a = 4
b = 3

print('{} + {} = {}'.format(a, b, a + b))
print('{} - {} = {}'.format(a, b, a - b))
print('{} * {} = {}'.format(a, b, a * b))
print('{} / {} = {:.2f}'.format(a, b, a / b)) # 限制小数点后两位
print('{} % {} = {}'.format(a, b, a % b))
print('{} // {} = {}'.format(a, b, a // b))
print('{} ** {} = {}'.format(a, b, a ** b))

# 输出（output）
4 + 3 = 7
4 - 3 = 1
4 * 3 = 12
4 / 3 = 1.33
4 % 3 = 1
4 // 3 = 1
4 ** 3 = 64

# 字符串与数字
radius = 10
pi = 3.14
area = pi * radius ** 2
formated_string = 'The area of a circle with a radius {} is {:.2f}.'.format(radius, area) # 小数点后保留 2 位
print(formated_string)

```

#### 字符串插值 / f-string（Python 3.6+）

另一种新的字符串格式化方式是字符串插值（string interpolation），即 f-string。字符串以 f 开头，我们可以在对应位置注入（inject）数据。

```py
a = 4
b = 3
print(f'{a} + {b} = {a +b}')
print(f'{a} - {b} = {a - b}')
print(f'{a} * {b} = {a * b}')
print(f'{a} / {b} = {a / b:.2f}')
print(f'{a} % {b} = {a % b}')
print(f'{a} // {b} = {a // b}')
print(f'{a} ** {b} = {a ** b}')
```

### Python 字符串作为字符序列

Python 字符串是字符（character）的序列（sequence），它们与 Python 其他有序对象序列（list 和 tuple）共享基本的访问方法。从字符串（以及任何序列）中提取单个字符的最简单方法，就是将它们解包（unpack）到对应的变量中。

#### 解包字符

```
language = 'Python'
a,b,c,d,e,f = language # 将序列中的字符解包到变量中
print(a) # P
print(b) # y
print(c) # t
print(d) # h
print(e) # o
print(f) # n
```

#### 通过索引访问字符串中的字符

在编程中，计数从零开始。因此，字符串的第一个字母位于零索引（zero index）处，字符串的最后一个字母位于字符串长度减一的位置。

![String index](../images/string_index.png)

```py
language = 'Python'
first_letter = language[0]
print(first_letter) # P
second_letter = language[1]
print(second_letter) # y
last_index = len(language) - 1
last_letter = language[last_index]
print(last_letter) # n
```

如果我们想从右端开始，可以使用负索引（negative indexing）。-1 是最后一个索引。

```py
language = 'Python'
last_letter = language[-1]
print(last_letter) # n
second_last = language[-2]
print(second_last) # o
```

#### 对 Python 字符串切片

在 Python 中，我们可以将字符串切片（slice）为子字符串（substring）。

```py
language = 'Python'
first_three = language[0:3] # 从索引 0 开始，直到 3 但不包括 3
print(first_three) #Pyt
last_three = language[3:6]
print(last_three) # hon
# 另一种方式
last_three = language[-3:]
print(last_three)   # hon
last_three = language[3:]
print(last_three)   # hon
```

#### 反转字符串

在 Python 中，我们可以轻松地反转（reverse）字符串。

```py
greeting = 'Hello, World!'
print(greeting[::-1]) # !dlroW ,olleH
```

#### 切片时跳过字符

在切片时，可以通过向切片方法传递步长（step）参数来跳过字符。

```py
language = 'Python'
pto = language[0:6:2] #
print(pto) # Pto
```

### 字符串方法

有许多字符串方法可以让我们对字符串进行格式化。请看以下示例中的部分字符串方法：

- capitalize(): 将字符串的第一个字符转换为大写字母（capital letter）

```py
challenge = 'thirty days of python'
print(challenge.capitalize()) # 'Thirty days of python'
```

- count(): 返回子字符串在字符串中出现的次数（occurrences），count(substring, start=.., end=..)。start 是计数的起始索引，end 是计数的最后一个索引。

```py
challenge = 'thirty days of python'
print(challenge.count('y')) # 3
print(challenge.count('y', 7, 14)) # 1, 
print(challenge.count('th')) # 2`
```

- endswith(): 检查字符串是否以指定的结尾结尾

```py
challenge = 'thirty days of python'
print(challenge.endswith('on'))   # True
print(challenge.endswith('tion')) # False
```

- expandtabs(): 将制表符（tab）字符替换为空格，默认 tab 大小为 8。它接受 tab size 参数

```py
challenge = 'thirty\tdays\tof\tpython'
print(challenge.expandtabs())   # 'thirty  days    of      python'
print(challenge.expandtabs(10)) # 'thirty    days      of        python'
```

- find(): 返回子字符串首次出现的索引，如果未找到则返回 -1

```py
challenge = 'thirty days of python'
print(challenge.find('y'))  # 5
print(challenge.find('th')) # 0
```

- rfind(): 返回子字符串最后一次出现的索引，如果未找到则返回 -1

```py
challenge = 'thirty days of python'
print(challenge.rfind('y'))  # 16
print(challenge.rfind('th')) # 17
```

- format(): 将字符串格式化为更美观的输出  
   关于字符串格式的更多内容，请查看此[链接](https://www.programiz.com/python-programming/methods/string/format)

```py
first_name = 'Asabeneh'
last_name = 'Yetayeh'
age = 250
job = 'teacher'
country = 'Finland'
sentence = 'I am {} {}. I am a {}. I am {} years old. I live in {}.'.format(first_name, last_name, job, age, country)
print(sentence) # I am Asabeneh Yetayeh. I am 250 years old. I am a teacher. I live in Finland.

radius = 10
pi = 3.14
area = pi * radius ** 2
result = 'The area of a circle with radius {} is {}'.format(str(radius), str(area))
print(result) # The area of a circle with radius 10 is 314
```

- index(): 返回子字符串的最低索引（lowest index），附加参数指示起始和结束索引（默认为 0 和字符串长度减 1）。如果未找到子字符串，会抛出 ValueError。

```py
challenge = 'thirty days of python'
sub_string = 'da'
print(challenge.index(sub_string))  # 7
print(challenge.index(sub_string, 9)) # 错误（error）
```

- rindex(): 返回子字符串的最高索引（highest index），附加参数指示起始和结束索引（默认为 0 和字符串长度减 1）

```py
challenge = 'thirty days of python'
sub_string = 'da'
print(challenge.rindex(sub_string))  # 7
print(challenge.rindex(sub_string, 9)) # 错误（error）
print(challenge.rindex('on', 8)) # 19
```

- isalnum(): 检查是否为字母数字（alphanumeric）字符

```py
challenge = 'ThirtyDaysPython'
print(challenge.isalnum()) # True

challenge = '30DaysPython'
print(challenge.isalnum()) # True

challenge = 'thirty days of python'
print(challenge.isalnum()) # False，空格不是字母数字字符

challenge = 'thirty days of python 2019'
print(challenge.isalnum()) # False
```

- isalpha(): 检查字符串中的所有元素是否都是字母字符（a-z 和 A-Z）

```py
challenge = 'thirty days of python'
print(challenge.isalpha()) # False，空格再次被排除
challenge = 'ThirtyDaysPython'
print(challenge.isalpha()) # True
num = '123'
print(num.isalpha())      # False
```

- isdecimal(): 检查字符串中的所有字符是否都是十进制数字（0-9）

```py
challenge = 'thirty days of python'
print(challenge.isdecimal())  # False
challenge = '123'
print(challenge.isdecimal())  # True
challenge = '²'
print(challenge.isdigit())   # True 
challenge = '12 3'
print(challenge.isdecimal())  # False，不允许有空格
```

- isdigit(): 检查字符串中的所有字符是否都是数字（0-9 以及其他一些表示数字的 unicode 字符）

```py
challenge = 'Thirty'
print(challenge.isdigit()) # False
challenge = '30'
print(challenge.isdigit())   # True
challenge = '²'
print(challenge.isdigit())   # True
```

- isnumeric(): 检查字符串中的所有字符是否都是数字或与数字相关的内容（与 isdigit() 类似，但接受更多符号，如 ½）

```py
num = '10'
print(num.isnumeric()) # True
num = '½' # ½
print(num.isnumeric()) # True
num = '10.5'
print(num.isnumeric()) # False
```

- isidentifier(): 检查是否为有效的标识符（identifier）——即检查字符串是否是合法的变量名

```py
challenge = '30DaysOfPython'
print(challenge.isidentifier()) # False，因为以数字开头
challenge = 'thirty_days_of_python'
print(challenge.isidentifier()) # True
```

- islower(): 检查字符串中的所有字母字符是否都是小写（lowercase）

```py
challenge = 'thirty days of python'
print(challenge.islower()) # True
challenge = 'Thirty days of python'
print(challenge.islower()) # False
```

- isupper(): 检查字符串中的所有字母字符是否都是大写（uppercase）

```py
challenge = 'thirty days of python'
print(challenge.isupper()) #  False
challenge = 'THIRTY DAYS OF PYTHON'
print(challenge.isupper()) # True
```

- join(): 返回一个拼接后的字符串

```py
web_tech = ['HTML', 'CSS', 'JavaScript', 'React']
result = ' '.join(web_tech)
print(result) # 'HTML CSS JavaScript React'
```

```py
web_tech = ['HTML', 'CSS', 'JavaScript', 'React']
result = '# '.join(web_tech)
print(result) # 'HTML# CSS# JavaScript# React'
```

- strip(): 移除字符串开头和结尾处所有指定的字符

```py
challenge = 'thirty days of pythoonnn'
print(challenge.strip('noth')) # 'irty days of py'
```

- replace(): 用给定的字符串替换子字符串

```py
challenge = 'thirty days of python'
print(challenge.replace('python', 'coding')) # 'thirty days of coding'
```

- split(): 使用给定的字符串或空格作为分隔符（separator）来分割字符串

```py
challenge = 'thirty days of python'
print(challenge.split()) # ['thirty', 'days', 'of', 'python']
challenge = 'thirty, days, of, python'
print(challenge.split(', ')) # ['thirty', 'days', 'of', 'python']
```

- title(): 返回一个标题格式（title cased）的字符串

```py
challenge = 'thirty days of python'
print(challenge.title()) # Thirty Days Of Python
```

- swapcase(): 将所有大写字符转换为小写，并将所有小写字符转换为大写

```py
challenge = 'thirty days of python'
print(challenge.swapcase())   # THIRTY DAYS OF PYTHON
challenge = 'Thirty Days Of Python'
print(challenge.swapcase())  # tHIRTY dAYS oF pYTHON
```

- startswith(): 检查字符串是否以指定的字符串开头

```py
challenge = 'thirty days of python'
print(challenge.startswith('thirty')) # True

challenge = '30 days of python'
print(challenge.startswith('thirty')) # False
```

🌕 你是一个非凡的人，拥有非凡的潜力。你刚刚完成了第 4 天的挑战，在通往伟大的道路上已经领先了四步。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 4 天

1. 将字符串 'Thirty'、'Days'、'Of'、'Python' 拼接成一个字符串，'Thirty Days Of Python'。
2. 将字符串 'Coding'、'For'、'All' 拼接成一个字符串，'Coding For All'。
3. 声明（Declare）一个名为 company 的变量，并为其赋初始值 "Coding For All"。
4. 使用 _print()_ 打印变量 company。
5. 使用 _len()_ 方法和 _print()_ 打印 company 字符串的长度。
6. 使用 _upper()_ 方法将所有字符改为大写字母。
7. 使用 _lower()_ 方法将所有字符改为小写字母。
8. 使用 capitalize()、title()、swapcase() 方法来格式化字符串 _Coding For All_ 的值。
9. 切下（slice）_Coding For All_ 字符串的第一个单词。
10. 使用 index、find 或其他方法检查 _Coding For All_ 字符串是否包含单词 Coding。
11. 将字符串 'Coding For All' 中的单词 coding 替换为 Python。
12. 使用 replace 方法或其他方法将 "Python for Everyone" 改为 "Python for All"。
13. 使用空格作为分隔符来分割（split）字符串 'Coding For All'。
14. "Facebook, Google, Microsoft, Apple, IBM, Oracle, Amazon" 在逗号处分割该字符串。
15. 字符串 _Coding For All_ 中索引 0 处的字符是什么。
16. 字符串 _Coding For All_ 的最后一个索引是什么。
17. 字符串 "Coding For All" 中索引 10 处的字符是什么。
18. 为 'Python For Everyone' 创建一个首字母缩写词（acronym）或缩写（abbreviation）。
19. 为 'Coding For All' 创建一个首字母缩写词或缩写。
20. 使用 index 确定字母 C 在 Coding For All 中首次出现的位置。
21. 使用 index 确定字母 F 在 Coding For All 中首次出现的位置。
22. 使用 rfind 确定字母 l 在 Coding For All People 中最后一次出现的位置。
23. 使用 index 或 find 找出单词 'because' 在以下句子中首次出现的位置：'You cannot end a sentence with because because because is a conjunction'
24. 使用 rindex 找出单词 because 在以下句子中最后一次出现的位置：'You cannot end a sentence with because because because is a conjunction'
25. 在以下句子中切出（slice out）短语 'because because because'：'You cannot end a sentence with because because because is a conjunction'
26. 找出单词 'because' 在以下句子中首次出现的位置：'You cannot end a sentence with because because because is a conjunction'
27. 在以下句子中切出短语 'because because because'：'You cannot end a sentence with because because because is a conjunction'
28. 'Coding For All' 是否以子字符串 _Coding_ 开头？
29. 'Coding For All' 是否以子字符串 _coding_ 结尾？
30. '&nbsp;&nbsp; Coding For All &nbsp;&nbsp;&nbsp; &nbsp;'，移除给定字符串左右两端的尾随空格（trailing spaces）。
31. 以下哪个变量在使用 isidentifier() 方法时会返回 True：
    - 30DaysOfPython
    - thirty_days_of_python
32. 以下列表包含一些 Python 库的名称：['Django', 'Flask', 'Bottle', 'Pyramid', 'Falcon']。用井号加空格（hash with space）字符串连接该列表。
33. 使用换行转义序列分隔以下句子。
    ```py
    I am enjoying this challenge.
    I just wonder what is next.
    ```
34. 使用制表符转义序列编写以下行。
    ```py
    Name      Age     Country   City
    Asabeneh  250     Finland   Helsinki
    ```
35. 使用字符串格式化方法显示以下内容：

```sh
radius = 10
area = 3.14 * radius ** 2
The area of a circle with radius 10 is 314 meters square.
```

36. 使用字符串格式化方法完成以下内容：

```sh
8 + 6 = 14
8 - 6 = 2
8 * 6 = 48
8 / 6 = 1.33
8 % 6 = 2
8 // 6 = 1
8 ** 6 = 262144
```

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 3 天](../03_Day_Operators/03_operators.md) | [第 5 天](../05_Day_Lists/05_lists.md)
