<div align="center">
  <h1> 🐍 30 Days Of Python：第 8 天 - 字典（Dictionaries）</h1>
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

[<< 第 7 天](../07_Day_Sets/07_sets_集合.md) | [第 9 天 >>](../09_Day_Conditionals/09_conditionals_条件语句.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 8 天](#-第-8-天)
  - [字典（Dictionaries）](#字典dictionaries)
    - [创建字典](#创建字典)
    - [字典的长度](#字典的长度)
    - [访问字典元素](#访问字典元素)
    - [向字典添加元素](#向字典添加元素)
    - [修改字典中的元素](#修改字典中的元素)
    - [检查字典中的键](#检查字典中的键)
    - [从字典中移除键值对](#从字典中移除键值对)
    - [将字典转换为元素列表](#将字典转换为元素列表)
    - [清空字典](#清空字典)
    - [删除字典](#删除字典)
    - [复制字典](#复制字典)
    - [获取字典的键列表](#获取字典的键列表)
    - [获取字典的值列表](#获取字典的值列表)
  - [💻 练习 - 第 8 天](#-练习---第-8-天)

# 📘 第 8 天

## 字典（Dictionaries）

Dictionary（字典）是一种无序的、可修改的（mutable）、成对的（key: value）数据类型集合。

### 创建字典

要创建字典，我们使用花括号 {} 或 *dict()* 内置函数。

```py
# 语法
empty_dict = {}
# 带有数据值的字典
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
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
```

上面的字典表明，值可以是任何数据类型：字符串（string）、布尔值（boolean）、列表（list）、元组（tuple）、集合（set）或字典。

### 字典的长度

它检查字典中"键值对"的数量。

```py
# 语法
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
print(len(dct)) # 4
```

**示例：**

```py
person = {
    'first_name':'Asabeneh',
    'last_name':'Yetayeh',
    'age':250,
    'country':'Finland',
    'is_married':True,
    'skills':['JavaScript', 'React', 'Node', 'MongoDB', 'Python'],
    'address':{
        'street':'Space street',
        'zipcode':'02210'
    }
    }
print(len(person)) # 7

```

### 访问字典元素

我们可以通过键名来访问字典元素。

```py
# 语法
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
print(dct['key1']) # value1
print(dct['key4']) # value4
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
print(person['first_name']) # Asabeneh
print(person['country'])    # Finland
print(person['skills'])     # ['JavaScript', 'React', 'Node', 'MongoDB', 'Python']
print(person['skills'][0])  # JavaScript
print(person['address']['street']) # Space street
print(person['city'])       # 错误（Error）
```

通过键名访问元素时，如果键不存在会抛出错误。为了避免这个错误，我们需要先检查键是否存在，或者使用 _get_ 方法。如果键不存在，get 方法返回 None（一种 NoneType 对象数据类型）。
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
print(person.get('first_name')) # Asabeneh
print(person.get('country'))    # Finland
print(person.get('skills')) #['JavaScript', 'React', 'Node', 'MongoDB', 'Python']
print(person.get('city'))   # None
```

### 向字典添加元素

我们可以向字典添加新的键值对。

```py
# 语法
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
dct['key5'] = 'value5'
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
person['job_title'] = 'Instructor'
person['skills'].append('HTML')
print(person)
```

### 修改字典中的元素

我们可以修改字典中的元素。

```py
# 语法
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
dct['key1'] = 'value-one'
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
person['first_name'] = 'Eyob'
person['age'] = 252
```

### 检查字典中的键

我们使用 _in_ 运算符来检查字典中是否存在某个键。

```py
# 语法
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
print('key2' in dct) # True
print('key5' in dct) # False
```

### 从字典中移除键值对

- _pop(key)_: 移除指定键名的元素：
- _popitem()_: 移除最后一个元素
- _del_: 移除指定键名的元素

```py
# 语法
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
dct.pop('key1') # 移除 key1 元素
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
dct.popitem() # 移除最后一个元素
del dct['key2'] # 移除 key2 元素
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
person.pop('first_name')        # 移除 firstname 元素
person.popitem()                # 移除 address 元素
del person['is_married']        # 移除 is_married 元素
```

### 将字典转换为元素列表

_items()_ 方法将字典转换为元组（tuple）列表。

```py
# 语法
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
print(dct.items()) # dict_items([('key1', 'value1'), ('key2', 'value2'), ('key3', 'value3'), ('key4', 'value4')])
```

### 清空字典

如果我们不想要字典中的元素，可以使用 _clear()_ 方法清空它们。

```py
# 语法
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
print(dct.clear()) # None
```

### 删除字典

如果我们不再使用某个字典，可以将其完全删除。

```py
# 语法
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
del dct
```

### 复制字典

我们可以使用 _copy()_ 方法复制字典。使用 copy 可以避免对原始字典的修改（mutation）。

```py
# 语法
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
dct_copy = dct.copy() # {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
```

### 获取字典的键列表

_keys()_ 方法将字典的所有键以列表形式返回。

```py
# 语法
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
keys = dct.keys()
print(keys)     # dict_keys(['key1', 'key2', 'key3', 'key4'])
```

### 获取字典的值列表

_values()_ 方法将字典的所有值以列表形式返回。

```py
# 语法
dct = {'key1':'value1', 'key2':'value2', 'key3':'value3', 'key4':'value4'}
values = dct.values()
print(values)     # dict_values(['value1', 'value2', 'value3', 'value4'])
```

🌕 你令人惊叹。现在，你已经充满了字典的力量。你刚刚完成了第 8 天的挑战，在通往伟大的道路上已经领先了八步。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 8 天

1. 创建一个名为 dog 的空字典
2. 向 dog 字典添加 name、color、breed、legs、age
3. 创建一个 student 字典，并添加 first_name、last_name、gender、age、marital status、skills、country、city 和 address 作为字典的键
4. 获取 student 字典的长度
5. 获取 skills 的值并检查其数据类型，它应该是一个列表
6. 通过添加一到两个技能来修改 skills 的值
7. 获取字典的键列表
8. 获取字典的值列表
9. 使用 _items()_ 方法将字典转换为元组列表
10. 删除字典中的一个元素
11. 删除其中一个字典

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 7 天](../07_Day_Sets/07_sets_集合.md) | [第 9 天 >>](../09_Day_Conditionals/09_conditionals_条件语句.md)
