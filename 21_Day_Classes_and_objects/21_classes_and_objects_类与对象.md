<div align="center">
  <h1> 🐍 30 Days Of Python：第 21 天 - 类（Classes）与对象（Objects）</h1>
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

[<< 第 20 天](../20_Day_Python_package_manager/20_python_package_manager_Python包管理器.md) | [第 22 天 >>](../22_Day_Web_scraping/22_web_scraping_网络爬虫.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 21 天](#-第-21-天)
  - [类与对象](#类与对象)
    - [创建类](#创建类)
    - [创建对象](#创建对象)
    - [类构造函数](#类构造函数)
    - [对象方法](#对象方法)
    - [对象默认方法](#对象默认方法)
    - [用于修改类默认值的方法](#用于修改类默认值的方法)
    - [继承](#继承)
    - [重写父类方法](#重写父类方法)
  - [💻 练习 - 第 21 天](#-练习---第-21-天)
    - [练习：第 1 级](#练习第-1-级)
    - [练习：第 2 级](#练习第-2-级)
    - [练习：第 3 级](#练习第-3-级)

# 📘 第 21 天

## 类与对象

Python 是一门面向对象编程（object oriented programming）语言。Python 中的一切都是对象（object），拥有自己的属性（property）和方法（method）。程序中使用的数字（number）、字符串（string）、列表（list）、字典（dictionary）、元组（tuple）、集合（set）等，都是相应内置类（built-in class）的对象。我们创建类（class）是为了创建对象。类就像是对象的构造器（constructor），或者说是创建对象的"蓝图（blueprint）"。我们通过实例化（instantiate）类来创建对象。类定义了对象的属性和行为，而对象则代表了该类。

从一开始，我们就在不知不觉地使用类和对象了。Python 程序中的每个元素都是一个类的对象。
让我们检查一下 Python 中的所有内容是否都是类：

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> num = 10
>>> type(num)
<class 'int'>
>>> string = 'string'
>>> type(string)
<class 'str'>
>>> boolean = True
>>> type(boolean)
<class 'bool'>
>>> lst = []
>>> type(lst)
<class 'list'>
>>> tpl = ()
>>> type(tpl)
<class 'tuple'>
>>> set1 = set()
>>> type(set1)
<class 'set'>
>>> dct = {}
>>> type(dct)
<class 'dict'>
```

### 创建类

要创建类，我们需要使用关键字 **class**，后跟名称和冒号。类名应该使用 **CamelCase** 命名法。

```sh
# 语法
class ClassName:
  code goes here
```

**示例（Example）：**

```py
class Person:
  pass
print(Person)
```

```sh
<__main__.Person object at 0x10804e510>
```

### 创建对象

我们可以通过调用类来创建对象。

```py
p = Person()
print(p)
```

### 类构造函数

在上面的示例中，我们已经从 Person 类创建了一个对象。然而，没有构造函数的类在实际应用中并不真正有用。让我们使用构造函数（constructor function）让我们的类更加实用。如同 Java 或 JavaScript 中的构造函数，Python 也有一个内置的 **__init__**() 构造函数。**__init__** 构造函数有一个 self 参数，它是对类当前实例的引用。
**示例：**

```py
class Person:
      def __init__ (self, name):
        # self 允许将参数附加到类上
          self.name =name

p = Person('Asabeneh')
print(p.name)
print(p)
```

```sh
# 输出（output）
Asabeneh
<__main__.Person object at 0x2abf46907e80>
```

让我们向构造函数添加更多参数。

```py
class Person:
      def __init__(self, firstname, lastname, age, country, city):
          self.firstname = firstname
          self.lastname = lastname
          self.age = age
          self.country = country
          self.city = city


p = Person('Asabeneh', 'Yetayeh', 250, 'Finland', 'Helsinki')
print(p.firstname)
print(p.lastname)
print(p.age)
print(p.country)
print(p.city)
```

```sh
# 输出（output）
Asabeneh
Yetayeh
250
Finland
Helsinki
```

### 对象方法

对象可以拥有方法（methods）。方法是属于对象的函数（functions）。

**示例：**

```py
class Person:
      def __init__(self, firstname, lastname, age, country, city):
          self.firstname = firstname
          self.lastname = lastname
          self.age = age
          self.country = country
          self.city = city
      def person_info(self):
        return f'{self.firstname} {self.lastname} is {self.age} years old. He lives in {self.city}, {self.country}'

p = Person('Asabeneh', 'Yetayeh', 250, 'Finland', 'Helsinki')
print(p.person_info())
```

```sh
# 输出（output）
Asabeneh Yetayeh is 250 years old. He lives in Helsinki, Finland
```

### 对象默认方法

有时，你可能希望对象方法具有默认值。如果我们为构造函数中的参数提供默认值，就可以避免在调用或实例化类时不传参数而产生错误。让我们看看它的样子：

**示例：**

```py
class Person:
      def __init__(self, firstname='Asabeneh', lastname='Yetayeh', age=250, country='Finland', city='Helsinki'):
          self.firstname = firstname
          self.lastname = lastname
          self.age = age
          self.country = country
          self.city = city

      def person_info(self):
        return f'{self.firstname} {self.lastname} is {self.age} years old. He lives in {self.city}, {self.country}.'

p1 = Person()
print(p1.person_info())
p2 = Person('John', 'Doe', 30, 'Nomanland', 'Noman city')
print(p2.person_info())
```

```sh
# 输出（output）
Asabeneh Yetayeh is 250 years old. He lives in Helsinki, Finland.
John Doe is 30 years old. He lives in Noman city, Nomanland.
```

### 用于修改类默认值的方法

在下面的示例中，person 类的所有构造函数参数都有默认值。除此之外，我们还有一个 skills 参数，可以通过方法访问它。让我们创建 add_skill 方法来向 skills 列表添加技能。

```py
class Person:
      def __init__(self, firstname='Asabeneh', lastname='Yetayeh', age=250, country='Finland', city='Helsinki'):
          self.firstname = firstname
          self.lastname = lastname
          self.age = age
          self.country = country
          self.city = city
          self.skills = []

      def person_info(self):
        return f'{self.firstname} {self.lastname} is {self.age} years old. He lives in {self.city}, {self.country}.'
      def add_skill(self, skill):
          self.skills.append(skill)

p1 = Person()
print(p1.person_info())
p1.add_skill('HTML')
p1.add_skill('CSS')
p1.add_skill('JavaScript')
p2 = Person('John', 'Doe', 30, 'Nomanland', 'Noman city')
print(p2.person_info())
print(p1.skills)
print(p2.skills)
```

```sh
# 输出（output）
Asabeneh Yetayeh is 250 years old. He lives in Helsinki, Finland.
John Doe is 30 years old. He lives in Noman city, Nomanland.
['HTML', 'CSS', 'JavaScript']
[]
```

### 继承

使用继承（inheritance），我们可以复用父类（parent class）的代码。继承允许我们定义一个从父类继承所有方法和属性的类。父类或超类（super class）或基类（base class）是提供所有方法和属性的类。子类（child class）是从另一个类或父类继承的类。
让我们通过继承 person 类来创建一个 student 类。

```py
class Student(Person):
    pass


s1 = Student('Eyob', 'Yetayeh', 30, 'Finland', 'Helsinki')
s2 = Student('Lidiya', 'Teklemariam', 28, 'Finland', 'Espoo')
print(s1.person_info())
s1.add_skill('JavaScript')
s1.add_skill('React')
s1.add_skill('Python')
print(s1.skills)

print(s2.person_info())
s2.add_skill('Organizing')
s2.add_skill('Marketing')
s2.add_skill('Digital Marketing')
print(s2.skills)

```

```sh
output
Eyob Yetayeh is 30 years old. He lives in Helsinki, Finland.
['JavaScript', 'React', 'Python']
Lidiya Teklemariam is 28 years old. He lives in Espoo, Finland.
['Organizing', 'Marketing', 'Digital Marketing']
```

我们没有在子类中调用 **__init__**() 构造函数。如果我们没有调用它，我们仍然可以从父类访问所有属性。但如果我们调用了构造函数，我们可以通过调用 _super_ 来访问父类属性。
我们可以向子类添加新方法，也可以通过创建与父类同名的方法来重写（override）父类的方法。当我们添加 **__init__**() 函数时，子类将不再继承父类的 **__init__**() 函数。

### 重写父类方法（多态）

```py
class Student(Person):
    def __init__ (self, firstname='Asabeneh', lastname='Yetayeh',age=250, country='Finland', city='Helsinki', gender='male'):
        self.gender = gender
        super().__init__(firstname, lastname,age, country, city)
    def person_info(self):
        gender = 'He' if self.gender =='male' else 'She'
        return f'{self.firstname} {self.lastname} is {self.age} years old. {gender} lives in {self.city}, {self.country}.'

s1 = Student('Eyob', 'Yetayeh', 30, 'Finland', 'Helsinki','male')
s2 = Student('Lidiya', 'Teklemariam', 28, 'Finland', 'Espoo', 'female')
print(s1.person_info())
s1.add_skill('JavaScript')
s1.add_skill('React')
s1.add_skill('Python')
print(s1.skills)

print(s2.person_info())
s2.add_skill('Organizing')
s2.add_skill('Marketing')
s2.add_skill('Digital Marketing')
print(s2.skills)
```

```sh
Eyob Yetayeh is 30 years old. He lives in Helsinki, Finland.
['JavaScript', 'React', 'Python']
Lidiya Teklemariam is 28 years old. She lives in Espoo, Finland.
['Organizing', 'Marketing', 'Digital Marketing']
```

我们可以使用 super() 内置函数或父类名称 Person 来自动从父类继承方法和属性。在上面的示例中，我们重写了父类方法。子类方法有不同的功能，它可以识别性别是男性还是女性，并分配适当的代词（He/She），这体现了面向对象中多态这一性质。

### 类对象
类本身作为一个特殊对象，拥有：类属性、类方法

```python
class Demo:
	# 类属性
	name = "类属性名"
	
	# 类方法
	@classmethod
	def 类方法名(cls): # 与self相似，cls记录类地址
		cls.name = "张三"

# 调用
Demo.类方法名
```

### 私有属性和私有方法

```python
class Traitor:
    def __init__(self, name):
        self.__name = name
        
    def __antiPRC(self):
        print("***")
    
    def a(self):
        print (self.__name)
        self.__antiPRC()

teacherLi = Traitor("李老师")
print(teacherLi.__name) # 代码报错
teacherLi.__antiPRC() # 代码报错
teracherLi.a()

# 查看对象的所有可用方法（私有的不在其中但是有重命名的实现，防君子不防小人）
print(dir(teacherLi))
# ['_Traitor__antiPRC', '_Traitor__name', '__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getstate__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'a']

```

### 类的方法间的变量的作用域
```python
class A:
    def __init__(self):
        pass

    def m1(self):
        self.v1 = 10
        v2=20

    def m2(self):
        # v1带self，他的作用域是当前类，v2没有带self，作用域是当前方法
        print(self.v1)
        # print(v2) 不能运行

if __name__ == '__main__':
    a = A()
    a.m1()
    a.m2()
```

🌕 现在，你已充满编程的超能力。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 21 天

### 练习：第 1 级

1. Python 有一个名为 _statistics_ 的模块（module），我们可以使用这个模块来进行所有的统计计算。然而，为了学习如何创建函数和复用函数，让我们尝试开发一个程序，计算样本的集中趋势度量（mean、median、mode）和变异性度量（range、variance、standard deviation）。除了这些度量之外，还要找出样本的 min、max、count、percentile 和 frequency distribution。你可以创建一个名为 Statistics 的类，并将所有进行统计计算的函数作为 Statistics 类的方法。请检查下面的输出。

```py
ages = [31, 26, 34, 37, 27, 26, 32, 32, 26, 27, 27, 24, 32, 33, 27, 25, 26, 38, 37, 31, 34, 24, 33, 29, 26]

print('Count:', data.count()) # 25
print('Sum: ', data.sum()) # 744
print('Min: ', data.min()) # 24
print('Max: ', data.max()) # 38
print('Range: ', data.range()) # 14
print('Mean: ', data.mean()) # 30
print('Median: ', data.median()) # 29
print('Mode: ', data.mode()) # {'mode': 26, 'count': 5}
print('Standard Deviation: ', data.std()) # 4.2
print('Variance: ', data.var()) # 17.5
print('Frequency Distribution: ', data.freq_dist()) # [(20.0, 26), (16.0, 27), (12.0, 32), (8.0, 37), (8.0, 34), (8.0, 33), (8.0, 31), (8.0, 24), (4.0, 38), (4.0, 29), (4.0, 25)]
```

```sh
# 你的输出应该看起来像这样
print(data.describe())
Count: 25
Sum:  744
Min:  24
Max:  38
Range:  14
Mean:  30
Median:  29
Mode:  (26, 5)
Variance:  17.5
Standard Deviation:  4.2
Frequency Distribution: [(20.0, 26), (16.0, 27), (12.0, 32), (8.0, 37), (8.0, 34), (8.0, 33), (8.0, 31), (8.0, 24), (4.0, 38), (4.0, 29), (4.0, 25)]
```

### 练习：第 2 级

1. 创建一个名为 PersonAccount 的类。它有 firstname、lastname、incomes、expenses 属性，以及 total_income、total_expense、account_info、add_income、add_expense 和 account_balance 方法。incomes 是一组收入及其描述。expenses 也是如此。

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 20 天](../20_Day_Python_package_manager/20_python_package_manager_Python包管理器.md) | [第 22 天 >>](../22_Day_Web_scraping/22_web_scraping_网络爬虫.md)
