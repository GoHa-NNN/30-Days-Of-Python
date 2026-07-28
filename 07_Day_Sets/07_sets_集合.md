<div align="center">
  <h1> 🐍 30 Days Of Python：第 7 天 - 集合（Sets）</h1>
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

[<< 第 6 天](../06_Day_Tuples/06_tuples_元组.md) | [第 8 天 >>](../08_Day_Dictionaries/08_dictionaries_字典.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 7 天](#-第-7-天)
  - [集合（Sets）](#集合sets)
    - [创建集合](#创建集合)
    - [获取集合的长度](#获取集合的长度)
    - [访问集合中的元素](#访问集合中的元素)
    - [检查元素是否存在](#检查元素是否存在)
    - [向集合添加元素](#向集合添加元素)
    - [从集合中移除元素](#从集合中移除元素)
    - [清空集合中的元素](#清空集合中的元素)
    - [删除集合](#删除集合)
    - [将列表转换为集合](#将列表转换为集合)
    - [合并集合](#合并集合)
    - [查找交集元素](#查找交集元素)
    - [检查子集和超集](#检查子集和超集)
    - [检查两个集合之间的差集](#检查两个集合之间的差集)
    - [查找两个集合之间的对称差集](#查找两个集合之间的对称差集)
    - [合并集合](#合并集合-1)
  - [💻 练习 - 第 7 天](#-练习---第-7-天)
    - [练习：第 1 级](#练习第-1-级)
    - [练习：第 2 级](#练习第-2-级)
    - [练习：第 3 级](#练习第-3-级)

# 📘 第 7 天

## 集合（Sets）

Set（集合）是一组元素的集合。让我带你回到小学或高中的数学课堂。数学中集合的定义同样可以应用在 Python 中。集合是一组无序（unordered）且无索引（un-indexed）的互异元素（distinct elements）。在 Python 中，集合用于存储唯一的元素，并且可以在多个集合之间查找并集（union）、交集（intersection）、差集（difference）、对称差集（symmetric difference）、子集（subset）、超集（super set）以及不相交集合（disjoint set）。

### 创建集合

要创建空集合，我们使用 set() 函数。空花括号 {} 会创建一个字典（dictionary）。

- 创建空集合

```py
# 语法（syntax）
st = set()
```

- 创建带有初始元素的集合

```py
# 语法
st = {'item1', 'item2', 'item3', 'item4'}
```

**示例（Example）：**

```py
# 语法
fruits = {'banana', 'orange', 'mango', 'lemon'}
```

### 获取集合的长度

我们使用 **len()** 方法来获取集合的长度。

```py
# 语法
st = {'item1', 'item2', 'item3', 'item4'}
len(st)
```

**示例：**

```py
fruits = {'banana', 'orange', 'mango', 'lemon'}
len(fruits)
```

### 访问集合中的元素

我们使用循环（loop）来访问元素。我们将在循环章节中看到这部分内容。

### 检查元素是否存在

要检查某个元素是否存在于集合中，我们使用 _in_ 成员运算符（membership operator）。

```py
# 语法
st = {'item1', 'item2', 'item3', 'item4'}
print("集合 st 是否包含 item3？", 'item3' in st) # 集合 st 是否包含 item3？ True
```

**示例：**

```py
fruits = {'banana', 'orange', 'mango', 'lemon'}
print('mango' in fruits ) # True
```

### 向集合添加元素

集合一旦创建，我们就不能修改其中的元素，但可以添加新的元素。

- 使用 _add()_ 添加单个元素

```py
# 语法
st = {'item1', 'item2', 'item3', 'item4'}
st.add('item5')
```

**示例：**

```py
fruits = {'banana', 'orange', 'mango', 'lemon'}
fruits.add('lime')
```

- 使用 _update()_ 添加多个元素
  _update()_ 允许向集合添加多个元素。_update()_ 接受一个列表（list）作为参数。

```py
# 语法
st = {'item1', 'item2', 'item3', 'item4'}
st.update(['item5','item6','item7'])
```

**示例：**

```py
fruits = {'banana', 'orange', 'mango', 'lemon'}
vegetables = ('tomato', 'potato', 'cabbage','onion', 'carrot')
fruits.update(vegetables)
```

### 从集合中移除元素

我们可以使用 _remove()_ 方法从集合中移除元素。如果元素不存在，_remove()_ 方法会抛出错误（error），因此最好先检查该元素是否存在于给定的集合中。而 _discard()_ 方法不会抛出任何错误。

```py
# 语法
st = {'item1', 'item2', 'item3', 'item4'}
st.remove('item2')
```

pop() 方法会从列表中随机移除一个元素，并返回被移除的元素。

**示例：**

```py
fruits = {'banana', 'orange', 'mango', 'lemon'}
fruits.pop()  # 从集合中随机移除一个元素

```

如果我们对被移除的元素感兴趣。

```py
fruits = {'banana', 'orange', 'mango', 'lemon'}
removed_item = fruits.pop()
```

### 清空集合中的元素

如果我们想清空或清空集合，可以使用 _clear_ 方法。

```py
# 语法
st = {'item1', 'item2', 'item3', 'item4'}
st.clear()
```

**示例：**

```py
fruits = {'banana', 'orange', 'mango', 'lemon'}
fruits.clear()
print(fruits) # set()
```

### 删除集合

如果我们想删除集合本身，可以使用 _del_ 运算符。

```py
# 语法
st = {'item1', 'item2', 'item3', 'item4'}
del st
```

**示例：**

```py
fruits = {'banana', 'orange', 'mango', 'lemon'}
del fruits
```

### 将列表转换为集合

我们可以将列表转换为集合，也可以将集合转换为列表。将列表转换为集合会移除重复项，只保留唯一的元素。

```py
# 语法
lst = ['item1', 'item2', 'item3', 'item4', 'item1']
st = set(lst)  # {'item2', 'item4', 'item1', 'item3'} - 顺序是随机的，因为集合通常是无序的
```

**示例：**

```py
fruits = ['banana', 'orange', 'mango', 'lemon','orange', 'banana']
fruits = set(fruits) # {'mango', 'lemon', 'banana', 'orange'}
```

### 合并集合

我们可以使用 _union()_ 或 _update()_ 方法或 _|_ 符号来合并两个集合。

- 并集（Union）
  此方法返回一个新集合

```py
# 语法
st1 = {'item1', 'item2', 'item3', 'item4'}
st2 = {'item5', 'item6', 'item7', 'item8'}
st3 = st1.union(st2) #st3 = st1 | st2
```

**示例：**

```py
fruits = {'banana', 'orange', 'mango', 'lemon'}
vegetables = {'tomato', 'potato', 'cabbage','onion', 'carrot'}
print(fruits.union(vegetables)) # {'lemon', 'carrot', 'tomato', 'banana', 'mango', 'orange', 'cabbage', 'potato', 'onion'}
# 或者使用：print(fruits | vegetables)
```

- 更新（Update）
  此方法将一个集合插入到给定的集合中

```py
# 语法
st1 = {'item1', 'item2', 'item3', 'item4'}
st2 = {'item5', 'item6', 'item7', 'item8'}
st1.update(st2) # st2 的内容被添加到 st1 中
```

**示例：**

```py
fruits = {'banana', 'orange', 'mango', 'lemon'}
vegetables = {'tomato', 'potato', 'cabbage','onion', 'carrot'}
fruits.update(vegetables)
print(fruits) # {'lemon', 'carrot', 'tomato', 'banana', 'mango', 'orange', 'cabbage', 'potato', 'onion'}
```

### 查找交集元素

交集（Intersection）返回两个集合中都存在的元素组成的集合，也可以使用 _&_ 符号。请看示例：

```py
# 语法
st1 = {'item1', 'item2', 'item3', 'item4'}
st2 = {'item3', 'item2'}
st1.intersection(st2) # {'item3', 'item2'}
# 或者使用：st1 & st2
```

**示例：**

```py
whole_numbers = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
even_numbers = {0, 2, 4, 6, 8, 10}
whole_numbers.intersection(even_numbers) # {0, 2, 4, 6, 8, 10}

python = {'p', 'y', 't', 'h', 'o','n'}
dragon = {'d', 'r', 'a', 'g', 'o','n'}
python.intersection(dragon)     # {'o', 'n'}
# python & dragon
```

### 检查子集和超集

一个集合可以是其他集合的子集（subset）或超集（super set）：

- 子集：_issubset()_
- 超集：_issuperset_

```py
# 语法
st1 = {'item1', 'item2', 'item3', 'item4'}
st2 = {'item2', 'item3'}
st2.issubset(st1) # True
st1.issuperset(st2) # True
```

**示例：**

```py
whole_numbers = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
even_numbers = {0, 2, 4, 6, 8, 10}
whole_numbers.issubset(even_numbers) # False，因为它是超集
whole_numbers.issuperset(even_numbers) # True

python = {'p', 'y', 't', 'h', 'o','n'}
dragon = {'d', 'r', 'a', 'g', 'o','n'}
python.issubset(dragon)     # False
```

### 检查两个集合之间的差集

它返回两个集合之间的差集，也可以使用 _-_ 符号。

```py
# 语法
st1 = {'item1', 'item2', 'item3', 'item4'}
st2 = {'item2', 'item3'}
st2.difference(st1) # set() : st2 - st1
st1.difference(st2) # {'item1', 'item4'} => st1\st2  : st2 - st1
```

**示例：**

```py
whole_numbers = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
even_numbers = {0, 2, 4, 6, 8, 10}
whole_numbers.difference(even_numbers) # {1, 3, 5, 7, 9}

python = {'p', 'y', 't', 'o','n'}
dragon = {'d', 'r', 'a', 'g', 'o','n'}
python.difference(dragon)     # {'p', 'y', 't'}  - 结果是无序的（集合的特性）
# python - dragon
dragon.difference(python)     # {'d', 'r', 'a', 'g'}
# dragon - python
```

### 查找两个集合之间的对称差集

它返回两个集合之间的对称差集（symmetric difference）。也就是说，它返回一个包含两个集合中所有元素的集合，但排除同时存在于两个集合中的元素，数学上表示为：(A\B) ∪ (B\A)

```py
# 语法
st1 = {'item1', 'item2', 'item3', 'item4'}
st2 = {'item2', 'item3'}
# 即 (A\B)∪(B\A)
st2.symmetric_difference(st1) # {'item1', 'item4'} : st2 ^ st1
```

**示例：**

```py
whole_numbers = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
some_numbers = {1, 2, 3, 4, 5}
whole_numbers.symmetric_difference(some_numbers) # {0, 6, 7, 8, 9, 10}

python = {'p', 'y', 't', 'h', 'o','n'}
dragon = {'d', 'r', 'a', 'g', 'o','n'}
python.symmetric_difference(dragon)  # {'r', 't', 'p', 'y', 'g', 'a', 'd', 'h'}
# python ^ dragon
```

### 合并集合

如果两个集合没有共同的元素，我们称它们为不相交集合（disjoint sets）。我们可以使用 _isdisjoint()_ 方法检查两个集合是否相交或不相交。

```py
# 语法
st1 = {'item1', 'item2', 'item3', 'item4'}
st2 = {'item2', 'item3'}
st2.isdisjoint(st1) # False
```

**示例：**

```py
even_numbers = {0, 2, 4 ,6, 8}
odd_numbers = {1, 3, 5, 7, 9}
even_numbers.isdisjoint(odd_numbers) # True，因为没有共同元素

python = {'p', 'y', 't', 'h', 'o','n'}
dragon = {'d', 'r', 'a', 'g', 'o','n'}
python.isdisjoint(dragon)  # False，存在共同元素 {'o', 'n'}
```

🌕 你是一颗冉冉升起的新星。你刚刚完成了第 7 天的挑战，在通往伟大的道路上已经领先了七步。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 7 天

```py
# 集合
it_companies = {'Facebook', 'Google', 'Microsoft', 'Apple', 'IBM', 'Oracle', 'Amazon'}
A = {19, 22, 24, 20, 25, 26}
B = {19, 22, 20, 25, 26, 24, 28, 27}
age = [22, 19, 24, 25, 26, 24, 25, 24]
```

### 练习：第 1 级

1. 求集合 it_companies 的长度
2. 向 it_companies 添加 'Twitter'
3. 向集合 it_companies 一次性插入多家 IT 公司
4. 从集合 it_companies 中移除一家公司
5. remove 和 discard 之间有什么区别

### 练习：第 2 级

1. 合并 A 和 B
2. 求 A 与 B 的交集
3. A 是否是 B 的子集
4. A 和 B 是否是不相交集合
5. 将 A 与 B 合并，以及将 B 与 A 合并
6. A 和 B 之间的对称差集是什么
7. 完全删除这些集合

### 练习：第 3 级

1. 将年龄列表转换为集合，并比较列表和集合的长度，哪个更大？
2. 解释以下数据类型之间的区别：字符串（string）、列表（list）、元组（tuple）和集合（set）
3. _I am a teacher and I love to inspire and teach people._ 这个句子中有多少个唯一的单词？使用 split 方法和集合来获取唯一的单词。

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 6 天](../06_Day_Tuples/06_tuples_元组.md) | [第 8 天 >>](../08_Day_Dictionaries/08_dictionaries_字典.md)
