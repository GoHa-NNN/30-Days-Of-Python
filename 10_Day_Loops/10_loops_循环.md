<div align="center">
  <h1> 🐍 30 Days Of Python：第 10 天 - 循环（Loops）</h1>
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

[<< 第 9 天](../09_Day_Conditionals/09_conditionals_条件语句.md) | [第 11 天 >>](../11_Day_Functions/11_functions_函数.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 10 天](#-第-10-天)
  - [循环（Loops）](#循环loops)
    - [while 循环](#while-循环)
    - [Break 与 Continue - 第 1 部分](#break-与-continue---第-1-部分)
    - [for 循环](#for-循环)
    - [Break 与 Continue - 第 2 部分](#break-与-continue---第-2-部分)
    - [range 函数](#range-函数)
    - [嵌套 for 循环](#嵌套-for-循环)
    - [for else](#for-else)
    - [pass](#pass)
  - [💻 练习 - 第 10 天](#-练习---第-10-天)
    - [练习：第 1 级](#练习第-1-级)
    - [练习：第 2 级](#练习第-2-级)
    - [练习：第 3 级](#练习第-3-级)

# 📘 第 10 天

## 循环（Loops）

生活充满了日常惯例。在编程中，我们也会做大量重复性的任务。为了处理重复性任务，编程语言使用循环。Python 编程语言也提供了以下两种循环：

1. while 循环（while loop）
2. for 循环（for loop）

### while 循环

我们使用保留字 _while_ 来创建 while 循环。它用于重复执行一段代码块，直到给定的条件（condition）不再满足。当条件变为假（false）时，循环后面的代码行将继续执行。

```py
  # 语法
while condition:
    code goes here
```

**示例：**

```py
count = 0
while count < 5:
    print(count)
    count = count + 1
# 从 0 打印到 4
```

在上面的 while 循环中，当 count 等于 5 时，条件变为假，循环随之停止。
如果我们希望在条件不再为真时也能运行一段代码块，可以使用 _else_。

```py
  # 语法
while condition:
    code goes here
else:
    code goes here
```

**示例：**

```py
count = 0
while count < 5:
    print(count)
    count = count + 1
else:
    print(count)
```

上面的循环条件在 count 等于 5 时为假，循环停止，开始执行 else 语句。因此会打印出 5。

### Break 与 Continue - 第 1 部分

- Break（跳出）：当我们想退出或停止循环时使用 break。

```py
# 语法
while condition:
    code goes here
    if another_condition:
        break
```

**示例：**

```py
count = 0
while count < 5:
    print(count)
    count = count + 1
    if count == 3:
        break
```

上面的 while 循环只打印 0、1、2，但当到达 3 时就停止了。

- Continue（继续）：使用 continue 语句可以跳过当前迭代（iteration），继续执行下一次迭代：

```py
  # 语法
while condition:
    code goes here
    if another_condition:
        continue
```

**示例：**

```py
count = 0
while count < 5:
    if count == 3:
        count += 1
        continue
    print(count)
    count = count + 1
```

上面的 while 循环只打印 0、1、2 和 4（跳过了 3）。

### for 循环

_for_ 关键字用于创建 for 循环，与其他编程语言类似，但在语法上有一些差异。循环用于遍历（iterate over）一个序列（sequence）（可以是列表、元组、字典、集合或字符串）。

- 在列表上使用 for 循环

```py
# 语法
for iterator in lst:
    code goes here
```

**示例：**

```py
numbers = [0, 1, 2, 3, 4, 5]
for number in numbers: # number 是临时名称，用于引用列表中的元素，仅在此循环内有效
    print(number)       # 数字将逐行打印，从 0 到 5
```

- 在字符串上使用 for 循环

```py
# 语法
for iterator in string:
    code goes here
```

**示例：**

```py
language = 'Python'
for letter in language:
    print(letter)


for i in range(len(language)):
    print(language[i])
```

- 在元组上使用 for 循环

```py
# 语法
for iterator in tpl:
    code goes here
```

**示例：**

```py
numbers = (0, 1, 2, 3, 4, 5)
for number in numbers:
    print(number)
```

- 与字典一起使用 for 循环
  遍历字典会获取字典的键（key）。

```py
  # 语法
for iterator in dct:
    code goes here
```

**示例：**

```py
person = {
    'first_name':'Asabeneh',
    'last_name':'Yetayeh',
    'age':250,
    'country':'Finland',
    'is_marred':True,
    'skills':['JavaScript', 'React', 'Node', 'MongoDB', 'Python'],
    'address':{
        'street':'Space street',
        'zipcode':'02210'
    }
}
for key in person:
    print(key)

for key, value in person.items():
    print(key, value) # 这样我们可以同时打印出键和值
```

- 在集合上使用 for 循环

```py
# 语法
for iterator in st:
    code goes here
```

**示例：**

```py
it_companies = {'Facebook', 'Google', 'Microsoft', 'Apple', 'IBM', 'Oracle', 'Amazon'}
for company in it_companies:
    print(company)
```

### Break 与 Continue - 第 2 部分

简短回顾：
_Break_（跳出）：我们想在循环完成之前停止循环时使用 break。

```py
# 语法
for iterator in sequence:
    code goes here
    if condition:
        break
```

**示例：**

```py
numbers = (0,1,2,3,4,5)
for number in numbers:
    print(number)
    if number == 3:
        break
```

在上面的示例中，循环在到达 3 时停止。

Continue（继续）：当我们想在循环的迭代过程中跳过某些步骤时使用 continue。

```py
  # 语法
for iterator in sequence:
    code goes here
    if condition:
        continue
```

**示例：**

```py
numbers = (0,1,2,3,4,5)
for number in numbers:
    print(number)
    if number == 3:
        continue
    print('Next number should be ', number + 1) if number != 5 else print("loop's end") # 简短的条件判断需要同时使用 if 和 else 语句
print('outside the loop')
```

在上面的示例中，如果数字等于 3，则条件之后（但在循环内）的步骤会被跳过，如果还有剩余迭代，循环将继续执行。

### range 函数

_range()_ 函数用于返回一个数字列表。_range(start, end, step)_ 接受三个参数：起始值、结束值和增量。默认情况下，它从 0 开始，增量为 1。range 序列至少需要 1 个参数（end）。

使用 range 创建序列

```py
lst = list(range(11))
print(lst) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
st = set(range(1, 11))    # 2 个参数表示序列的起始和结束，步长默认为 1
print(st) # {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}

lst = list(range(0,11,2))
print(lst) # [0, 2, 4, 6, 8, 10]
st = set(range(0,11,2))
print(st) #  {0, 2, 4, 6, 8, 10}

# 从起始到结束的倒序
lst = list(range(11,0,-2))
print(lst) # [11,9,7,5,3,1]
```

```py
# 语法
for iterator in range(start, end, step):
```

**示例：**

```py
for number in range(11):
    print(number)   # 打印 0 到 10，不包括 11
```

### 嵌套 for 循环

我们可以在循环内部再写循环。

```py
# 语法
for x in y:
    for t in x:
        print(t)
```

**示例：**

```py
person = {
    'first_name': 'Asabeneh',
    'last_name': 'Yetayeh',
    'age': 250,
    'country': 'Finland',
    'is_marred': True,
    'skills': ['JavaScript', 'React', 'Node', 'MongoDB', 'Python'],
    'address': {
        'street': 'Space street',
        'zipcode': '02210'
    }
}
for key in person:
    if key == 'skills':
        for skill in person['skills']:
            print(skill)
```

### for else

如果我们想在循环结束时执行某些提示信息，可以使用 else。

```py
# 语法
for iterator in range(start, end, step):
    do something
else:
    print('循环结束了')
```

**示例：**

```py
for number in range(11):
    print(number)   # 打印 0 到 10，不包括 11
else:
    print('循环停止于', number)
```

### pass

在 Python 中，当某个位置需要语句（在冒号之后）时，但我们不想执行任何代码，可以写上 _pass_ 来避免错误。我们也可以将它用作未来语句的占位符（placeholder）。

**示例：**

```py
for number in range(6):
    pass
```

🌕 你建立了一个重要的里程碑，你势不可挡。继续前进！你刚刚完成了第 10 天的挑战，在通往伟大的道路上已经领先了十步。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 10 天

### 练习：第 1 级

1. 使用 for 循环遍历 0 到 10，用 while 循环做同样的事。
2. 使用 for 循环遍历 10 到 0，用 while 循环做同样的事。
3. 编写一个循环，调用七次 print()，使输出呈现以下三角形：

   ```py
     #
     ##
     ###
     ####
     #####
     ######
     #######
   ```

4. 使用嵌套循环创建以下内容：

   ```sh
   # # # # # # # #
   # # # # # # # #
   # # # # # # # #
   # # # # # # # #
   # # # # # # # #
   # # # # # # # #
   # # # # # # # #
   # # # # # # # #
   ```

5. 打印以下模式：

   ```sh
   0 x 0 = 0
   1 x 1 = 1
   2 x 2 = 4
   3 x 3 = 9
   4 x 4 = 16
   5 x 5 = 25
   6 x 6 = 36
   7 x 7 = 49
   8 x 8 = 64
   9 x 9 = 81
   10 x 10 = 100
   ```

6. 使用 for 循环遍历列表 ['Python', 'Numpy','Pandas','Django', 'Flask'] 并打印出各个元素。
7. 使用 for 循环遍历 0 到 100，仅打印偶数
8. 使用 for 循环遍历 0 到 100，仅打印奇数

### 练习：第 2 级

1.  使用 for 循环遍历 0 到 100，并打印所有数字的和。

```sh
所有数字的和为 5050。
```

2. 使用 for 循环遍历 0 到 100，并打印所有偶数的和与所有奇数的和。

   ```sh
   所有偶数的和为 2550。所有奇数的和为 2500。
   ```

### 练习：第 3 级

1. 进入 data 文件夹，使用 [countries.py](https://github.com/Asabeneh/30-Days-Of-Python/blob/master/data/countries.py) 文件。遍历所有国家，提取所有包含单词 _land_ 的国家。
2. 这是一个水果列表，['banana', 'orange', 'mango', 'lemon']，使用循环将其顺序反转。
3. 进入 data 文件夹，使用 [countries_data.py](https://github.com/Asabeneh/30-Days-Of-Python/blob/master/data/countries-data.py) 文件。
   1. 数据中总共有多少种语言
   2. 从数据中找出使用人数最多的十种语言
   3. 找出世界上人口最多的 10 个国家

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 9 天](../09_Day_Conditionals/09_conditionals_条件语句.md) | [第 11 天 >>](../11_Day_Functions/11_functions_函数.md)
