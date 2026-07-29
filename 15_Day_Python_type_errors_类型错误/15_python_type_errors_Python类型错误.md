<div align="center">
  <h1> 🐍 30 Days Of Python：第 15 天 - Python 类型错误（Python Type Errors）</h1>
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

[<< 第 14 天](../14_Day_Higher_order_functions_高阶函数/14_higher_order_functions_高阶函数.md) | [第 16 天 >>](../16_Day_Python_date_time_日期时间/16_python_datetime_Python日期时间.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)
- [📘 第 15 天](#-第-15-天)
  - [Python 错误类型（Error Types）](#python-错误类型error-types)
    - [SyntaxError](#syntaxerror)
    - [NameError](#nameerror)
    - [IndexError](#indexerror)
    - [ModuleNotFoundError](#modulenotfounderror)
    - [AttributeError](#attributeerror)
    - [KeyError](#keyerror)
    - [TypeError](#typeerror)
    - [ImportError](#importerror)
    - [ValueError](#valueerror)
    - [ZeroDivisionError](#zerodivisionerror)
  - [💻 练习：第 15 天](#-练习第-15-天)

# 📘 第 15 天

## Python 错误类型（Error Types）

当我们编写代码时，出现拼写错误或其他常见错误是很常见的。如果我们的代码无法运行，Python 解释器将显示一条消息，其中包含有关问题发生位置和错误类型的反馈信息。它有时也会给我们提供可能的修复建议。了解编程语言中不同类型的错误将帮助我们快速调试代码，也让我们在所做的事情上变得更好。

让我们逐一看看最常见的错误类型。首先让我们打开 Python 交互式解释器（interactive shell）。转到你的电脑终端并输入 'python'。Python 交互式解释器将被打开。

### SyntaxError

**示例 1：SyntaxError**

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print 'hello world'
  File "<stdin>", line 1
    print 'hello world'
                      ^
SyntaxError: Missing parentheses in call to 'print'. Did you mean print('hello world')?
>>>
```

正如你所看到的，我们犯了一个语法错误（SyntaxError），因为我们忘记用括号括起字符串，Python 已经给出了解决建议。让我们修复它。

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print 'hello world'
  File "<stdin>", line 1
    print 'hello world'
                      ^
SyntaxError: Missing parentheses in call to 'print'. Did you mean print('hello world')?
>>> print('hello world')
hello world
>>>
```

错误是一个 _SyntaxError_。修复后，我们的代码顺利执行了。让我们看看更多错误类型。

### NameError

**示例 1：NameError**

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print(age)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'age' is not defined
>>>
```

正如你从上面的消息中看到的，名称 age 未定义。是的，我们确实没有定义 age 变量，但我们试图打印它，就好像已经声明了它一样。现在，让我们通过声明它并赋值来修复这个问题。

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> print(age)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'age' is not defined
>>> age = 25
>>> print(age)
25
>>>
```

错误类型是 _NameError_。我们通过定义变量名来调试了这个错误。

### IndexError

**示例 1：IndexError**

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> numbers = [1, 2, 3, 4, 5]
>>> numbers[5]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
>>>
```

在上面的例子中，Python 抛出了一个 _IndexError_，因为列表只有从 0 到 4 的索引，所以它超出了范围。

### ModuleNotFoundError

**示例 1：ModuleNotFoundError**

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import maths
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'maths'
>>>
```

在上面的例子中，我故意在 math 后面加了一个多余的 s，抛出了 _ModuleNotFoundError_。让我们通过移除 math 后面多余的 s 来修复它。

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import maths
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'maths'
>>> import math
>>>
```

我们修复了它，让我们使用 math 模块中的一些函数。

### AttributeError

**示例 1：AttributeError**

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import maths
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'maths'
>>> import math
>>> math.PI
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: module 'math' has no attribute 'PI'
>>>
```

正如你所看到的，我又犯了一个错误！我试图从 math 模块调用 PI 常量，而不是 pi。它抛出了一个属性错误（AttributeError），这意味着该属性在模块中不存在。让我们通过将 PI 改为 pi 来修复它。

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import maths
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'maths'
>>> import math
>>> math.PI
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: module 'math' has no attribute 'PI'
>>> math.pi
3.141592653589793
>>>
```

现在，当我们从 math 模块调用 pi 时，我们得到了结果。

### KeyError

**示例 1：KeyError**

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> users = {'name':'Asab', 'age':250, 'country':'Finland'}
>>> users['name']
'Asab'
>>> users['county']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'county'
>>>
```

正如你所看到的，用于获取字典值的键有拼写错误。所以，这是一个键错误（KeyError），修复方法相当直接。让我们来做吧！

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> user = {'name':'Asab', 'age':250, 'country':'Finland'}
>>> user['name']
'Asab'
>>> user['county']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'county'
>>> user['country']
'Finland'
>>>
```

我们调试了错误，代码运行了，我们得到了值。

### TypeError

**示例 1：TypeError**

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 4 + '3'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
>>>
```

在上面的例子中，抛出了 TypeError，因为我们不能将数字和字符串相加。第一个解决方案是将字符串转换为 int 或 float。另一个解决方案是将数字转换为字符串（结果将是 '43'）。让我们按照第一个修复方案来做。

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 4 + '3'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unsupported operand type(s) for +: 'int' and 'str'
>>> 4 + int('3')
7
>>> 4 + float('3')
7.0
>>>
```

错误被移除，我们得到了预期的结果。

### ImportError

**示例 1：ImportError**

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> from math import power
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ImportError: cannot import name 'power' from 'math'
>>>
```

math 模块中没有名为 power 的函数，它的名字是 _pow_。让我们纠正它：

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> from math import power
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ImportError: cannot import name 'power' from 'math'
>>> from math import pow
>>> pow(2,3)
8.0
>>>
```

### ValueError

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> int('12a')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: invalid literal for int() with base 10: '12a'
>>>
```

在这种情况下，我们无法将给定的字符串转换为数字，因为其中包含字母 'a'。

### ZeroDivisionError

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 1/0
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
>>>
```

我们不能将数字除以零。

我们已经涵盖了一些 Python 错误类型，如果你想了解更多，请查看 Python 文档中关于 Python 错误类型的内容。
如果你擅长阅读错误类型，那么你将能够快速修复 bug，你也会成为一名更好的程序员。

🌕 你正在脱颖而出。你已经走在了通往伟大的半路上。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习：第 15 天

1. 打开你的 Python 交互式解释器并尝试本节涵盖的所有示例。

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 14 天](../14_Day_Higher_order_functions_高阶函数/14_higher_order_functions_高阶函数.md) | [第 16 天 >>](../16_Day_Python_date_time_日期时间/16_python_datetime_Python日期时间.md)
