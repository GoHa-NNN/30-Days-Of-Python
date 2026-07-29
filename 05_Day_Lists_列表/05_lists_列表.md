<div align="center">
  <h1> 🐍 30 Days Of Python：第 5 天 - 列表（Lists）</h1>
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

[<< 第 4 天](../04_Day_Strings_字符串/04_strings_字符串.md) | [第 6 天 >>](../06_Day_Tuples_元组/06_tuples_元组.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [第 5 天](#第-5-天)
  - [列表（Lists）](#列表lists)
    - [如何创建列表](#如何创建列表)
    - [使用正索引访问列表项](#使用正索引访问列表项)
    - [使用负索引访问列表项](#使用负索引访问列表项)
    - [解包列表项](#解包列表项)
    - [对列表切片](#对列表切片)
    - [修改列表](#修改列表)
    - [检查列表中的项](#检查列表中的项)
    - [向列表添加项](#向列表添加项)
    - [向列表中插入项](#向列表中插入项)
    - [从列表中移除项](#从列表中移除项)
    - [使用 Pop 移除项](#使用-pop-移除项)
    - [使用 Del 移除项](#使用-del-移除项)
    - [清空列表项](#清空列表项)
    - [复制列表](#复制列表)
    - [连接列表](#连接列表)
    - [统计列表中的项数](#统计列表中的项数)
    - [查找项的索引](#查找项的索引)
    - [反转列表](#反转列表)
    - [对列表项排序](#对列表项排序)
  - [💻 练习：第 5 天](#-练习第-5-天)
    - [练习：第 1 级](#练习第-1-级)
    - [练习：第 2 级](#练习第-2-级)

# 第 5 天

## 列表（Lists）

Python 中有四种集合（collection）数据类型：

- List（列表）：有序且可更改（可修改）的集合。允许重复成员。
- Tuple（元组）：有序且不可更改或不可修改（不可变，immutable）的集合。允许重复成员。
- Set（集合）：无序、无索引且不可修改，但我们可以向集合添加新项。不允许重复成员。
- Dictionary（字典）：有序（Python 3.7+）、可更改（可修改）且有索引的集合。不允许重复成员。

列表是不同数据类型的有序且可修改（mutable）的集合。列表可以为空，也可以包含不同数据类型的项。

### 如何创建列表

在 Python 中，我们可以通过两种方式创建列表：

- 使用 list 内置函数

```py
# 语法
lst = list()
```

```py
empty_list = list() # 这是一个空列表，列表中没有项
print(len(empty_list)) # 0
```

- 使用方括号，[]

```py
# 语法
lst = []
```

```py
empty_list = [] # 这是一个空列表，列表中没有项
print(len(empty_list)) # 0
```

带有初始值的列表。我们使用 _len()_ 来获取列表的长度。

```py
fruits = ['banana', 'orange', 'mango', 'lemon']                     # 水果列表
vegetables = ['Tomato', 'Potato', 'Cabbage','Onion', 'Carrot']      # 蔬菜列表
animal_products = ['milk', 'meat', 'butter', 'yoghurt']             # 动物产品列表
web_techs = ['HTML', 'CSS', 'JS', 'React','Redux', 'Node', 'MongDB'] # Web 技术列表
countries = ['Finland', 'Estonia', 'Denmark', 'Sweden', 'Norway']

# 打印列表及其长度
print('Fruits:', fruits)
print('Number of fruits:', len(fruits))
print('Vegetables:', vegetables)
print('Number of vegetables:', len(vegetables))
print('Animal products:',animal_products)
print('Number of animal products:', len(animal_products))
print('Web technologies:', web_techs)
print('Number of web technologies:', len(web_techs))
print('Countries:', countries)
print('Number of countries:', len(countries))
```

```sh
output
Fruits: ['banana', 'orange', 'mango', 'lemon']
Number of fruits: 4
Vegetables: ['Tomato', 'Potato', 'Cabbage', 'Onion', 'Carrot']
Number of vegetables: 5
Animal products: ['milk', 'meat', 'butter', 'yoghurt']
Number of animal products: 4
Web technologies: ['HTML', 'CSS', 'JS', 'React', 'Redux', 'Node', 'MongDB']
Number of web technologies: 7
Countries: ['Finland', 'Estonia', 'Denmark', 'Sweden', 'Norway']
Number of countries: 5
```

- 列表可以包含不同数据类型的项

```py
 lst = ['Asabeneh', 250, True, {'country':'Finland', 'city':'Helsinki'}] # 包含不同数据类型的列表
```

### 使用正索引访问列表项

我们使用索引（index）访问列表中的每个项。列表索引从 0 下面的图片清楚地显示了索引从哪里开始
![List index](../images/list_index.png)

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
first_fruit = fruits[0] # 我们使用索引访问第一项
print(first_fruit)      # banana
second_fruit = fruits[1]
print(second_fruit)     # orange
last_fruit = fruits[3]
print(last_fruit) # lemon
# 最后一个索引
last_index = len(fruits) - 1
last_fruit = fruits[last_index]
```

### 使用负索引访问列表项

负索引（negative indexing）意味着从末尾开始，-1 表示最后一项，-2 表示倒数第二项。

![List negative indexing](../images/list_negative_indexing.png)

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
first_fruit = fruits[-4]
last_fruit = fruits[-1]
second_last = fruits[-2]
print(first_fruit)      # banana
print(last_fruit)       # lemon
print(second_last)      # mango
```

### 解包列表项

```py
lst = ['item1','item2','item3', 'item4', 'item5']
first_item, second_item, third_item, *rest = lst
print(first_item)     # item1
print(second_item)    # item2
print(third_item)     # item3
print(rest)           # ['item4', 'item5']

```

```py
# 第一个示例
fruits = ['banana', 'orange', 'mango', 'lemon','lime','apple']
first_fruit, second_fruit, third_fruit, *rest = fruits
print(first_fruit)     # banana
print(second_fruit)    # orange
print(third_fruit)     # mango
print(rest)           # ['lemon','lime','apple']
# 第二个关于解包列表的示例
first, second, third,*rest, tenth = [1,2,3,4,5,6,7,8,9,10]
print(first)          # 1
print(second)         # 2
print(third)          # 3
print(rest)           # [4,5,6,7,8,9]
print(tenth)          # 10
# 第三个关于解包列表的示例
countries = ['Germany', 'France','Belgium','Sweden','Denmark','Finland','Norway','Iceland','Estonia']
gr, fr, bg, sw, *scandic, es = countries
print(gr)
print(fr)
print(bg)
print(sw)
print(scandic)
print(es)
```

### 对列表切片

- 正索引：我们可以通过指定起始、结束和步长来指定正索引的范围，返回值将是一个新列表。（start 的默认值为 0，end 的默认值为 len(lst) - 1（最后一项），step 的默认值为 1）

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
all_fruits = fruits[0:4] # 它返回所有水果
# 这也会得到与上面相同的结果
all_fruits = fruits[0:] # 如果我们不设置停止位置，它会取走剩余的所有项
orange_and_mango = fruits[1:3] # 它不包含第一个索引
orange_mango_lemon = fruits[1:]
orange_and_lemon = fruits[::2] # 这里我们使用了第三个参数，步长。它会每隔一项取一个 - ['banana', 'mango']
```

- 负索引：我们可以通过指定起始、结束和步长来指定负索引的范围，返回值将是一个新列表。

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
all_fruits = fruits[-4:] # 它返回所有水果
orange_and_mango = fruits[-3:-1] # 它不包含最后一个索引，['orange', 'mango']
orange_mango_lemon = fruits[-3:] # 这将从 -3 开始到末尾，['orange', 'mango', 'lemon']
reverse_fruits = fruits[::-1] # 负步长将按逆序取列表，['lemon', 'mango', 'orange', 'banana']
```

### 修改列表

列表是可变的或可修改的有序项集合。让我们修改水果列表。

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits[0] = 'avocado'
print(fruits)       #  ['avocado', 'orange', 'mango', 'lemon']
fruits[1] = 'apple'
print(fruits)       #  ['avocado', 'apple', 'mango', 'lemon']
last_index = len(fruits) - 1
fruits[last_index] = 'lime'
print(fruits)        #  ['avocado', 'apple', 'mango', 'lime']
```

### 检查列表中的项

使用 *in* 运算符检查某项是否是列表的成员。请看下面的示例。

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
does_exist = 'banana' in fruits
print(does_exist)  # True
does_exist = 'lime' in fruits
print(does_exist)  # False
```

### 向列表添加项

要向现有列表的末尾添加项，我们使用 *append()* 方法。

```py
# 语法
lst = list()
lst.append(item)
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits.append('apple')
print(fruits)           # ['banana', 'orange', 'mango', 'lemon', 'apple']
fruits.append('lime')   # ['banana', 'orange', 'mango', 'lemon', 'apple', 'lime']
print(fruits)
```

### 向列表中插入项

我们可以使用 *insert()* 方法在列表的指定索引处插入单个项。注意其他项会向右移动。*insert()* 方法接受两个参数：索引和要插入的项。

```py
# 语法
lst = ['item1', 'item2']
lst.insert(index, item)
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits.insert(2, 'apple') # 在 orange 和 mango 之间插入 apple
print(fruits)           # ['banana', 'orange', 'apple', 'mango', 'lemon']
fruits.insert(3, 'lime')   # ['banana', 'orange', 'apple', 'lime', 'mango', 'lemon']
print(fruits)
```

### 从列表中移除项

remove 方法从列表中移除指定的项

```py
# 语法
lst = ['item1', 'item2']
lst.remove(item)
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon', 'banana']
fruits.remove('banana')
print(fruits)  # ['orange', 'mango', 'lemon', 'banana'] - 此方法移除列表中首次出现的项
fruits.remove('lemon')
print(fruits)  # ['orange', 'mango', 'banana']
```

### 使用 Pop 移除项

*pop()* 方法移除指定的索引（如果未指定索引，则移除最后一项）：

```py
# 语法
lst = ['item1', 'item2']
lst.pop()       # 最后一项
lst.pop(index)
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits.pop()
print(fruits)       # ['banana', 'orange', 'mango']

fruits.pop(0)
print(fruits)       # ['orange', 'mango']
```

### 使用 Del 移除项

*del* 关键字移除指定的索引，也可用于删除索引范围内的项。它还可以完全删除列表

```py
# 语法
lst = ['item1', 'item2']
del lst[index] # 仅删除单项
del lst        # 完全删除列表
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon', 'kiwi', 'lime']
del fruits[0]
print(fruits)       # ['orange', 'mango', 'lemon', 'kiwi', 'lime']
del fruits[1]
print(fruits)       # ['orange', 'lemon', 'kiwi', 'lime']
del fruits[1:3]     # 这会删除给定索引之间的项，所以不会删除索引为 3 的项！
print(fruits)       # ['orange', 'lime']
del fruits
print(fruits)       # 这应该给出：NameError: name 'fruits' is not defined
```

### 清空列表项

*clear()* 方法清空列表：

```py
# 语法
lst = ['item1', 'item2']
lst.clear()
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits.clear()
print(fruits)       # []
```

### 复制列表

可以通过将列表重新赋值给新变量来复制列表：list2 = list1。现在，list2 是 list1 的引用（reference），我们对 list2 所做的任何修改也会影响原始列表 list1。但在很多情况下，我们不希望修改原始列表，而是希望有一个不同的副本。避免上述问题的方法之一是使用 _copy()_。

```py
# 语法
lst = ['item1', 'item2']
lst_copy = lst.copy()
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits_copy = fruits.copy()
print(fruits_copy)       # ['banana', 'orange', 'mango', 'lemon']
```

### 连接列表

在 Python 中有多种方式连接（join 或 concatenate）两个或多个列表。

- 加号运算符（Plus Operator，+）

```py
# 语法
list3 = list1 + list2
```

```py
positive_numbers = [1, 2, 3, 4, 5]
zero = [0]
negative_numbers = [-5,-4,-3,-2,-1]
integers = negative_numbers + zero + positive_numbers
print(integers) # [-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]
fruits = ['banana', 'orange', 'mango', 'lemon']
vegetables = ['Tomato', 'Potato', 'Cabbage', 'Onion', 'Carrot']
fruits_and_vegetables = fruits + vegetables
print(fruits_and_vegetables ) # ['banana', 'orange', 'mango', 'lemon', 'Tomato', 'Potato', 'Cabbage', 'Onion', 'Carrot']
```

- 使用 extend() 方法连接
  *extend()* 方法允许将列表追加到列表中。请看下面的示例。

```py
# 语法
list1 = ['item1', 'item2']
list2 = ['item3', 'item4', 'item5']
list1.extend(list2) # ['item1', 'item2', 'item3', 'item4', 'item5']
```

```py
num1 = [0, 1, 2, 3]
num2= [4, 5, 6]
num1.extend(num2)
print('Numbers:', num1) # Numbers: [0, 1, 2, 3, 4, 5, 6]
negative_numbers = [-5,-4,-3,-2,-1]
positive_numbers = [1, 2, 3,4,5]
zero = [0]

negative_numbers.extend(zero)
negative_numbers.extend(positive_numbers)
print('Integers:', negative_numbers) # Integers: [-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]
fruits = ['banana', 'orange', 'mango', 'lemon']
vegetables = ['Tomato', 'Potato', 'Cabbage', 'Onion', 'Carrot']
fruits.extend(vegetables)
print('Fruits and vegetables:', fruits ) # Fruits and vegetables: ['banana', 'orange', 'mango', 'lemon', 'Tomato', 'Potato', 'Cabbage', 'Onion', 'Carrot']
```

### 统计列表中的项数

*count()* 方法返回某项在列表中出现的次数：

```py
# 语法
lst = ['item1', 'item2']
lst.count(item)
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
print(fruits.count('orange'))   # 1
ages = [22, 19, 24, 25, 26, 24, 25, 24]
print(ages.count(24))           # 3
```

### 查找项的索引

*index()* 方法返回列表中某项的索引：

```py
# 语法
lst = ['item1', 'item2']
lst.index(item)
```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
print(fruits.index('orange'))   # 1
ages = [22, 19, 24, 25, 26, 24, 25, 24]
print(ages.index(24))           # 2，首次出现的位置
```

### 反转列表

*reverse()* 方法反转列表的顺序。

```py
# 语法
lst = ['item1', 'item2']
lst.reverse()

```

```py
fruits = ['banana', 'orange', 'mango', 'lemon']
fruits.reverse()
print(fruits) # ['lemon', 'mango', 'orange', 'banana']
ages = [22, 19, 24, 25, 26, 24, 25, 24]
ages.reverse()
print(ages) # [24, 25, 24, 26, 25, 24, 19, 22]
```

### 对列表项排序

要对列表排序，我们可以使用 _sort()_ 方法或 _sorted()_ 内置函数。_sort()_ 方法按升序重新排列列表项，并修改原始列表。如果 _sort()_ 方法的 reverse 参数等于 true，它将按降序排列列表。

- sort()：此方法修改原始列表

  ```py
  # 语法
  lst = ['item1', 'item2']
  lst.sort()                # 升序
  lst.sort(reverse=True)    # 降序
  ```

  **示例：**

  ```py
  fruits = ['banana', 'orange', 'mango', 'lemon']
  fruits.sort()
  print(fruits)             # 按字母顺序排序，['banana', 'lemon', 'mango', 'orange']
  fruits.sort(reverse=True)
  print(fruits) # ['orange', 'mango', 'lemon', 'banana']
  ages = [22, 19, 24, 25, 26, 24, 25, 24]
  ages.sort()
  print(ages) #  [19, 22, 24, 24, 24, 25, 25, 26]

  ages.sort(reverse=True)
  print(ages) #  [26, 25, 25, 24, 24, 24, 22, 19]
  ```

  sorted()：返回排序后的列表，不修改原始列表
  **示例：**

  ```py
  fruits = ['banana', 'orange', 'mango', 'lemon']
  print(sorted(fruits))   # ['banana', 'lemon', 'mango', 'orange']
  # 逆序
  fruits = ['banana', 'orange', 'mango', 'lemon']
  fruits = sorted(fruits,reverse=True)
  print(fruits)     # ['orange', 'mango', 'lemon', 'banana']
  ```

🌕 你很勤奋，已经取得了相当大的成就。你刚刚完成了第 5 天的挑战，在通往伟大的道路上已经领先了五步。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习：第 5 天

### 练习：第 1 级

1. 声明一个空列表
2. 声明一个包含超过 5 个项的列表
3. 找出列表的长度
4. 获取列表的第一项、中间项和最后一项
5. 声明一个名为 mixed_data_types 的列表，放入你的（姓名、年龄、身高、婚姻状况、地址）
6. 声明一个名为 it_companies 的列表变量，并赋初值为 Facebook、Google、Microsoft、Apple、IBM、Oracle 和 Amazon
7. 使用 _print()_ 打印列表
8. 打印列表中公司的数量
9. 打印第一个、中间和最后一个公司
10. 修改其中一个公司后打印列表
11. 向 it_companies 添加一家 IT 公司
12. 在列表中间插入一家 IT 公司
13. 将其中一家 it_companies 的名称改为大写（IBM 除外！）
14. 用字符串 '#;&nbsp; ' 连接 it_companies
15. 检查某家公司是否存在于 it_companies 列表中
16. 使用 sort() 方法对列表进行排序
17. 使用 reverse() 方法将列表按降序反转
18. 切出列表中的前 3 家公司
19. 切出列表中的最后 3 家公司
20. 切出列表中间的 IT 公司
21. 移除列表中的第一家 IT 公司
22. 移除列表中间的 IT 公司
23. 移除列表中的最后一家 IT 公司
24. 移除所有 IT 公司
25. 销毁 IT 公司列表
26. 连接以下列表：

    ```py
    front_end = ['HTML', 'CSS', 'JS', 'React', 'Redux']
    back_end = ['Node','Express', 'MongoDB']
    ```

27. 在问题 26 连接列表后。复制连接的列表并将其赋值给变量 full_stack，然后在 Redux 之后插入 Python 和 SQL。

### 练习：第 2 级

1. 以下是 10 名学生年龄的列表：

```sh
ages = [19, 22, 19, 24, 20, 25, 26, 24, 25, 24]
```

- 对列表进行排序并找出最小和最大年龄
- 将最小年龄和最大年龄再次添加到列表中
- 找出中位数年龄（一个中间项或两个中间项除以二）
- 找出平均年龄（所有项的总和除以数量）
- 找出年龄范围（最大值减最小值）
- 比较 (min - average) 和 (max - average) 的值，使用 _abs()_ 方法

1. 在[国家列表](https://github.com/Asabeneh/30-Days-Of-Python/tree/master/data/countries.py)中找到中间的国家
1. 如果国家列表数量为偶数，则将其分成两个相等的列表；如果为奇数，则前半部分多一个国家。
1. ['China', 'Russia', 'USA', 'Finland', 'Sweden', 'Norway', 'Denmark']。解包前三个国家，其余的作为斯堪的纳维亚国家。

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 4 天](../04_Day_Strings_字符串/04_strings_字符串.md) | [第 6 天 >>](../06_Day_Tuples_元组/06_tuples_元组.md)
