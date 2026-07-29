<div align="center">
  <h1> 🐍 30 Days Of Python：第 17 天 - 异常处理、打包解包、展开、枚举与压缩</h1>
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

[<< 第 16 天](../16_Day_Python_date_time/16_python_datetime_Python日期时间.md) | [第 18 天 >>](../18_Day_Regular_expressions/18_regular_expressions_正则表达式.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 17 天](#-第-17-天)
  - [异常处理](#异常处理)
  - [在 Python 中打包和解包参数](#在python中打包和解包参数)
    - [解包](#解包)
      - [解包列表](#解包列表)
      - [解包字典](#解包字典)
    - [打包](#打包)
    - [打包列表](#打包列表)
      - [打包字典](#打包字典)
  - [在 Python 中展开](#在-python-中展开)
  - [枚举（Enumerate）](#枚举enumerate)
  - [压缩（Zip）](#压缩zip)
  - [💻 练习 - 第 17 天](#-练习---第-17-天)

# 📘 第 17 天

## 异常处理

Python 使用 _try_ 和 _except_ 来优雅地处理错误。错误的优雅退出（graceful exit）或优雅处理是一种简单的编程习惯用法——程序检测到严重的错误条件后，以受控的方式"优雅退出"。通常，程序会在终端或日志中打印描述性错误信息作为优雅退出的一部分，这使得我们的应用程序更加健壮（robust）。异常（exception）的原因通常在程序本身之外。异常的示例可能包括：输入错误、文件名错误、找不到文件、IO 设备故障。错误的优雅处理可以防止我们的应用程序崩溃。

我们已经在上一节中介绍了不同的 Python _error_（错误）类型。如果我们在程序中使用 _try_ 和 _except_，那么这些代码块中就不会抛出错误。

![Try and Except](../images/try_except.png)

```py
try:
    如果一切顺利，运行此代码块中的代码
except:
    如果出现问题，运行此代码块中的代码
```

**示例（Example）：**

```py
try:
    print(10 + '5')
except:
    print('Something went wrong')
```

在上面的示例中，第二个操作数是字符串（string）。我们可以将其改为 float 或 int 来与数字相加使其正常工作。但如果不做任何更改，第二个代码块 _except_ 将会被执行。

**示例（Example）：**

```py
try:
    name = input('Enter your name:')
    year_born = input('Year you were born:')
    age = 2019 - year_born
    print(f'You are {name}. And your age is {age}.')
except:
    print('Something went wrong')
```

```sh
Something went wrong
```

在上面的示例中，异常代码块会运行，但我们并不确切知道问题所在。为了分析问题，我们可以将不同的错误类型与 except 配合使用。

在下面的示例中，它将处理错误并告诉我们抛出了哪种错误。

```py
try:
    name = input('Enter your name:')
    year_born = input('Year you were born:')
    age = 2019 - year_born
    print(f'You are {name}. And your age is {age}.')
except TypeError:
    print('Type error occured')
except ValueError:
    print('Value error occured')
except ZeroDivisionError:
    print('zero division error occured')
```

```sh
Enter your name:Asabeneh
Year you born:1920
Type error occured
```

在上面的代码中，输出将是 _TypeError_。
现在，让我们添加一个额外的代码块：

```py
try:
    name = input('Enter your name:')
    year_born = input('Year you born:')
    age = 2019 - int(year_born)
    print(f'You are {name}. And your age is {age}.')
except TypeError:
    print('Type error occur')
except ValueError:
    print('Value error occur')
except ZeroDivisionError:
    print('zero division error occur')
else:
    print('I usually run with the try block')
finally:
    print('I alway run.')
```

```sh
Enter your name:Asabeneh
Year you born:1920
You are Asabeneh. And your age is 99.
I usually run with the try block
I alway run.
```

也可以将上面的代码缩写如下：

```py
try:
    name = input('Enter your name:')
    year_born = input('Year you born:')
    age = 2019 - int(year_born)
    print(f'You are {name}. And your age is {age}.')
except Exception as e:
    print(e)

```

## Assert 断言

Python 提供了 _assert_ 关键字（keyword），用于在代码中插入调试断言（assertion）。当断言条件为假时，程序会抛出 `AssertionError` 异常（exception），这是一种轻量级的"前置条件检查"手段。

```py
assert condition, error_message
```

**示例（Example）：**

```py
def divide(a, b):
    assert b != 0, "除数不能为零"
    return a / b

print(divide(10, 2))  # 5.0
print(divide(10, 0))  # AssertionError: 除数不能为零
```

### assert 与 if + raise 的区别

_assert_ 和手动 `if ... raise AssertionError` 效果类似，但更简洁。此外，assert 可以通过 Python 的 `-O`（优化）选项全局禁用，因此**仅应用于调试阶段的契约检查，不应用于运行时输入校验**。

**示例（Example）：**

```py
# ✅ 正确用法：检查程序内部逻辑（调试用）
def calculate_discount(price, discount):
    result = price * (1 - discount)
    assert 0 <= result <= price, "计算结果超出合理范围"
    return result

# ❌ 错误用法：校验用户输入（因为可能被 -O 禁用）
def set_age(age):
    assert age > 0, "年龄必须为正数"  # 不要用 assert 做输入校验！
    return age
```

### 常见使用场景

- 函数前置条件检查（参数类型、取值范围）
- 算法中间结果的合理性验证
- 单元测试中的简单断言（配合 `unittest` 或 pytest）

```py
# 检查列表非空后再处理
def get_first_item(items):
    assert len(items) > 0, "列表不能为空"
    return items[0]

# 检查函数返回值类型
def process(data):
    result = sorted(data)
    assert isinstance(result, list), "返回值必须是列表类型"
    return result
```

## 在Python中打包和解包参数

我们使用两个运算符（operator）：

- \* 用于元组（tuple）
- \*\* 用于字典（dict）

让我们以下面的例子来说明。它只接受参数（argument），但我们有一个列表。我们可以将列表解包并转换为参数。

### 解包

#### 解包列表

```py
def sum_of_five_nums(a, b, c, d, e):
    return a + b + c + d + e

lst = [1, 2, 3, 4, 5]
print(sum_of_five_nums(lst)) # TypeError: sum_of_five_nums() missing 4 required positional arguments: 'b', 'c', 'd', and 'e'
```

当我们运行这段代码时，它会抛出一个错误，因为这个函数接受数字（而不是列表）作为参数。让我们解包/解构（destructure）这个列表。

```py
def sum_of_five_nums(a, b, c, d, e):
    return a + b + c + d + e

lst = [1, 2, 3, 4, 5]
print(sum_of_five_nums(*lst))  # 15
```

我们也可以对 range 内置函数使用解包，该函数期望接收起始值和结束值。

```py
numbers = range(2, 7)  # 使用独立的参数进行常规调用
print(list(numbers)) # [2, 3, 4, 5, 6]
args = [2, 7]
numbers = range(*args)  # 使用从列表中解包的参数进行调用
print(numbers)      # [2, 3, 4, 5,6]

```

列表或元组也可以这样解包：

```py
countries = ['Finland', 'Sweden', 'Norway', 'Denmark', 'Iceland']
fin, sw, nor, *rest = countries
print(fin, sw, nor, rest)   # Finland Sweden Norway ['Denmark', 'Iceland']
numbers = [1, 2, 3, 4, 5, 6, 7]
one, *middle, last = numbers
print(one, middle, last)      #  1 [2, 3, 4, 5, 6] 7
```

#### 解包字典

```py
def unpacking_person_info(name, country, city, age):
    return f'{name} lives in {country}, {city}. He is {age} year old.'
dct = {'name':'Asabeneh', 'country':'Finland', 'city':'Helsinki', 'age':250}
print(unpacking_person_info(**dct)) # Asabeneh lives in Finland, Helsinki. He is 250 years old.
```

### 打包

有时我们永远不知道需要向 Python 函数传递多少个参数。我们可以使用打包（packing）方法，让我们的函数接受无限数量或任意数量的参数。

### 打包列表

```py
def sum_all(*args):
    s = 0
    for i in args:
        s += i
    return s
print(sum_all(1, 2, 3))             # 6
print(sum_all(1, 2, 3, 4, 5, 6, 7)) # 28
```

#### 打包字典

```py
def packing_person_info(**kwargs):
    # 检查 kwargs 的类型，它是 dict 类型
    # print(type(kwargs))
    # 打印字典项
    for key in kwargs:
        print(f"{key} = {kwargs[key]}")
    return kwargs

print(packing_person_info(name="Asabeneh",
      country="Finland", city="Helsinki", age=250))
```

```sh
name = Asabeneh
country = Finland
city = Helsinki
age = 250
{'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'age': 250}
```

## 在 Python 中展开

与 JavaScript 类似，在 Python 中也可以进行展开（spreading）。让我们通过下面的例子来验证：

```py
lst_one = [1, 2, 3]
lst_two = [4, 5, 6, 7]
lst = [0, *lst_one, *lst_two]
print(lst)          # [0, 1, 2, 3, 4, 5, 6, 7]
country_lst_one = ['Finland', 'Sweden', 'Norway']
country_lst_two = ['Denmark', 'Iceland']
nordic_countries = [*country_lst_one, *country_lst_two]
print(nordic_countries)  # ['Finland', 'Sweden', 'Norway', 'Denmark', 'Iceland']
```

## 枚举（Enumerate）

如果我们对列表的索引感兴趣，可以使用 _enumerate_ 内置函数来获取列表中每个项的索引。

```py
for index, item in enumerate([20, 30, 40]):
    print(index, item)
```

```py
countries = ['Finland', 'Sweden', 'Norway', 'Denmark', 'Iceland']
for index, i in enumerate(countries):
    if i == 'Finland':
        print(f'The country {i} has been found at index {index}')
```

```sh
The country Finland has been found at index 0.
```

## 压缩（Zip）

有时我们希望在遍历列表时将它们组合在一起。请看下面的示例：

```py
fruits = ['banana', 'orange', 'mango', 'lemon', 'lime']                    
vegetables = ['Tomato', 'Potato', 'Cabbage','Onion', 'Carrot']
fruits_and_veges = []
for f, v in zip(fruits, vegetables):
    fruits_and_veges.append({'fruit':f, 'veg':v})

print(fruits_and_veges)
```

```sh
[{'fruit': 'banana', 'veg': 'Tomato'}, {'fruit': 'orange', 'veg': 'Potato'}, {'fruit': 'mango', 'veg': 'Cabbage'}, {'fruit': 'lemon', 'veg': 'Onion'}, {'fruit': 'lime', 'veg': 'Carrot'}]
```

🌕 你意志坚定。在通往伟大的道路上，你已经领先了 17 步。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 17 天

1. names = ['Finland', 'Sweden', 'Norway','Denmark','Iceland', 'Estonia','Russia']。解包前五个国家并将它们存储在变量 nordic_countries 中，将 Estonia 和 Russia 分别存储在 es 和 ru 中。

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 16 天](../16_Day_Python_date_time/16_python_datetime_Python日期时间.md) | [第 18 天 >>](../18_Day_Regular_expressions/18_regular_expressions_正则表达式.md)
