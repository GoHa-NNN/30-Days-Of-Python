<div align="center">
  <h1> 🐍 30 Days Of Python：第 6 天 - 元组（Tuples）</h1>
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

[<< 第 5 天](../05_Day_Lists/05_lists_列表.md) | [第 7 天 >>](../07_Day_Sets/07_sets.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [第 6 天：](#第-6-天)
  - [元组（Tuples）](#元组tuples)
    - [创建元组](#创建元组)
    - [元组长度](#元组长度)
    - [访问元组项](#访问元组项)
    - [对元组切片](#对元组切片)
    - [将元组改为列表](#将元组改为列表)
    - [检查元组中的项](#检查元组中的项)
    - [连接元组](#连接元组)
    - [删除元组](#删除元组)
  - [💻 练习 - 第 6 天](#-练习---第-6-天)
    - [练习：第 1 级](#练习第-1-级)
    - [练习：第 2 级](#练习第-2-级)

# 第 6 天：

## 元组（Tuples）

元组是不同数据类型的有序且不可更改（不可变，immutable）的集合。元组使用圆括号 () 编写。一旦创建了元组，我们就无法更改它的值。我们不能在元组中使用 add、insert、remove 方法，因为它不可修改（mutable）。与 list 不同，元组的方法很少。与元组相关的方法：

- tuple(): 用于创建空元组
- count(): 用于统计元组中指定项的数量
- index(): 用于查找元组中指定项的索引
- `+` 运算符：用于连接两个或多个元组并创建新元组

### 创建元组

- 空元组：创建空元组

  ```py
  # 语法
  empty_tuple = ()
  # 或使用 tuple 构造函数
  empty_tuple = tuple()
  ```

- 带有初始值的元组

  ```py
  # 语法
  tpl = ('item1', 'item2','item3')
  ```

  ```py
  fruits = ('banana', 'orange', 'mango', 'lemon')
  ```

### 元组长度

我们使用 _len()_ 方法来获取元组的长度。

```py
# 语法
tpl = ('item1', 'item2', 'item3')
len(tpl)
```

### 访问元组项

- 正索引（Positive Indexing）
  与 list 数据类型类似，我们使用正索引或负索引来访问元组项。
  ![Accessing tuple items](../images/tuples_index.png)

  ```py
  # 语法
  tpl = ('item1', 'item2', 'item3')
  first_item = tpl[0]
  second_item = tpl[1]
  ```

  ```py
  fruits = ('banana', 'orange', 'mango', 'lemon')
  first_fruit = fruits[0]
  second_fruit = fruits[1]
  last_index =len(fruits) - 1
  last_fruit = fruits[last_index]
  ```

- 负索引（Negative indexing）
  负索引意味着从末尾开始，-1 表示最后一项，-2 表示倒数第二项，列表/元组长度的负值表示第一项。
  ![Tuple Negative indexing](../images/tuple_negative_indexing.png)

  ```py
  # 语法
  tpl = ('item1', 'item2', 'item3','item4')
  first_item = tpl[-4]
  second_item = tpl[-3]
  ```

  ```py
  fruits = ('banana', 'orange', 'mango', 'lemon')
  first_fruit = fruits[-4]
  second_fruit = fruits[-3]
  last_fruit = fruits[-1]
  ```

### 对元组切片

我们可以通过指定起始和结束索引范围来切出子元组，返回值将是一个包含指定项的新元组。

- 正索引范围

  ```py
  # 语法
  tpl = ('item1', 'item2', 'item3','item4')
  all_items = tpl[0:4]         # 所有项
  all_items = tpl[0:]         # 所有项
  middle_two_items = tpl[1:3]  # 不包含索引为 3 的项
  ```

  ```py
  fruits = ('banana', 'orange', 'mango', 'lemon')
  all_fruits = fruits[0:4]    # 所有项
  all_fruits= fruits[0:]      # 所有项
  orange_mango = fruits[1:3]  # 不包含索引为 3 的项
  orange_to_the_rest = fruits[1:]
  ```

- 负索引范围

  ```py
  # 语法
  tpl = ('item1', 'item2', 'item3','item4')
  all_items = tpl[-4:]         # 所有项
  middle_two_items = tpl[-3:-1]  # 不包含索引为 3 的项（-1）
  ```

  ```py
  fruits = ('banana', 'orange', 'mango', 'lemon')
  all_fruits = fruits[-4:]    # 所有项
  orange_mango = fruits[-3:-1]  # 不包含索引为 3 的项
  orange_to_the_rest = fruits[-3:]
  ```

### 将元组改为列表

我们可以将元组改为列表，也可以将列表改为元组。元组是不可变的，如果我们想修改元组，应该将其改为列表。

```py
# 语法
tpl = ('item1', 'item2', 'item3','item4')
lst = list(tpl)
```

```py
fruits = ('banana', 'orange', 'mango', 'lemon')
fruits = list(fruits)
fruits[0] = 'apple'
print(fruits)     # ['apple', 'orange', 'mango', 'lemon']
fruits = tuple(fruits)
print(fruits)     # ('apple', 'orange', 'mango', 'lemon')
```

### 检查元组中的项

我们可以使用 _in_ 检查某项是否存在于元组中，它返回一个布尔值（boolean）。

```py
# 语法
tpl = ('item1', 'item2', 'item3','item4')
'item2' in tpl # True
```

```py
fruits = ('banana', 'orange', 'mango', 'lemon')
print('orange' in fruits) # True
print('apple' in fruits) # False
fruits[0] = 'apple' # TypeError: 'tuple' object does not support item assignment
```

### 连接元组

我们可以使用 + 运算符连接两个或多个元组

```py
# 语法
tpl1 = ('item1', 'item2', 'item3')
tpl2 = ('item4', 'item5','item6')
tpl3 = tpl1 + tpl2
```

```py
fruits = ('banana', 'orange', 'mango', 'lemon')
vegetables = ('Tomato', 'Potato', 'Cabbage','Onion', 'Carrot')
fruits_and_vegetables = fruits + vegetables
```

### 删除元组

无法移除元组中的单个项，但可以使用 _del_ 删除元组本身。

```py
# 语法
tpl1 = ('item1', 'item2', 'item3')
del tpl1

```

```py
fruits = ('banana', 'orange', 'mango', 'lemon')
del fruits
```

🌕 你非常勇敢，走到了这一步。你刚刚完成了第 6 天的挑战，在通往伟大的道路上已经领先了六步。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 6 天

### 练习：第 1 级

1. 创建一个空元组
2. 创建一个包含你姐妹和兄弟名字的元组（虚构的兄弟姐妹也可以）
3. 将兄弟和姐妹元组连接并赋值给 siblings
4. 你有多少个兄弟姐妹？
5. 修改 siblings 元组，添加你父亲和母亲的名字，并赋值给 family_members

### 练习：第 2 级

1. 从 family_members 中解包兄弟姐妹和父母
1. 创建水果、蔬菜和动物产品元组。将这三个元组连接并赋值给名为 food_stuff_tp 的变量
1. 将 food_stuff_tp 元组改为 food_stuff_lt 列表
1. 从 food_stuff_tp 元组或 food_stuff_lt 列表中切出中间的一项或多项
1. 从 food_stuff_lt 列表中切出前三项和后三项
1. 完全删除 food_stuff_tp 元组
1. 检查元组中是否存在某项：

- 检查 'Estonia' 是否是北欧国家
- 检查 'Iceland' 是否是北欧国家

  ```py
  nordic_countries = ('Denmark', 'Finland','Iceland', 'Norway', 'Sweden')
  ```


[<< 第 5 天](../05_Day_Lists/05_lists_列表.md) | [第 7 天 >>](../07_Day_Sets/07_sets.md)
