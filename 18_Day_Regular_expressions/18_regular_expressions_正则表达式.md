<div align="center">
  <h1> 🐍 30 Days Of Python：第 18 天 - 正则表达式（Regular Expressions）</h1>
  <a class="header-badge" target="_blank" href="https://www.linkedin.com/in/asabeneh/">
  <img src="https://img.shields.io/badge/style--5eba00.svg?label=LinkedIn&logo=linkedin&style=social">
  </a>
  <a class="header-badge" target="_blank" href="https://twitter.com/Asabeneh">
  <img alt="Twitter Follow" src="https://img.shields.io/twitter/follow/asabeneh?style=social">
  </a>

<sub>作者（Author）：
<a href="https://www.linkedin.com/in/asabeneh/" target="_blank">Asabeneh Yetayeh</a><br>
<small>第一版（First Edition）：2019 年 11 月 22 日 - 12 月 22 日</small>
</sub>

</div>


[<< 第 17 天](../17_Day_Exception_handling/17_exception_handling_异常处理.md) | [第 19 天 >>](../19_Day_File_handling/19_file_handling_文件处理.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 18 天](#-第-18-天)
  - [正则表达式](#正则表达式)
    - [*re* 模块](#re-模块)
    - [*re* 模块中的方法](#re-模块中的方法)
      - [Match](#match)
      - [Search](#search)
      - [使用 *findall* 搜索所有匹配项](#使用-findall-搜索所有匹配项)
      - [替换子字符串](#替换子字符串)
  - [使用 RegEx Split 分割文本](#使用-regex-split-分割文本)
  - [编写 RegEx 模式](#编写-regex-模式)
    - [方括号](#方括号)
    - [RegEx 中的转义字符（\\）](#regex-中的转义字符)
    - [一次或多次（+）](#一次或多次)
    - [句号（.）](#句号)
    - [零次或多次（\*）](#零次或多次)
    - [零次或一次（?）](#零次或一次)
    - [RegEx 中的量词](#regex-中的量词)
    - [脱字符 ^](#脱字符-)
  - [💻 练习 - 第 18 天](#-练习---第-18-天)
    - [练习：第 1 级](#练习第-1-级)
    - [练习：第 2 级](#练习第-2-级)
    - [练习：第 3 级](#练习第-3-级)

# 📘 第 18 天

## 正则表达式

正则表达式（Regular Expression）或 RegEx 是一种特殊的文本字符串，用于帮助在数据中查找模式（pattern）。RegEx 可用于检查某种模式是否存在于不同的数据类型中。要在 Python 中使用 RegEx，首先我们应该导入名为 *re* 的 RegEx 模块。

### *re* 模块

导入模块后，我们可以使用它来检测或查找模式。

```py
import re
```

### *re* 模块中的方法

要查找模式，我们使用不同的 *re* 字符集（character set），它们允许在字符串中搜索匹配项。

- *re.match()*: 仅在第一行的开头搜索，如果找到则返回匹配对象（matched object），否则返回 None。
- *re.search*: 如果在字符串中的任何位置（包括多行字符串）存在匹配项，则返回一个匹配对象。
- *re.findall*: 返回包含所有匹配项的列表
- *re.split*: 接受一个字符串，在匹配点处将其分割，返回一个列表
- *re.sub*: 替换字符串中的一个或多个匹配项

#### Match

```py
# 语法
re.match(substring, string, re.I)
# substring 是字符串或模式，string 是我们查找模式的文本，re.I 表示忽略大小写
```

```py
import re

txt = 'I love to teach python and javaScript'
# 它返回一个包含 span 和 match 的对象
match = re.match('I love to teach', txt, re.I)
print(match)  # <re.Match object; span=(0, 15), match='I love to teach'>
# 我们可以使用 span 获取匹配的起始和结束位置，以元组形式返回
span = match.span()
print(span)     # (0, 15)
# 让我们从 span 中查找起始和结束位置
start, end = span
print(start, end)  # 0 15
substring = txt[start:end]
print(substring)       # I love to teach
```

从上面的示例可以看出，我们正在查找的模式（或子字符串）是 *I love to teach*。match 函数**仅**在文本以该模式开头时才返回对象。

```py
import re

txt = 'I love to teach python and javaScript'
match = re.match('I like to teach', txt, re.I)
print(match)  # None
```

该字符串不是以 *I like to teach* 开头的，因此没有匹配项，match 方法返回了 None。

#### Search

```py
# 语法
re.search(substring, string, re.I)
# substring 是模式，string 是我们查找模式的文本，re.I 是忽略大小写标志
```

```py
import re

txt = '''Python is the most beautiful language that a human being has ever created.
I recommend python for a first programming language'''

# 它返回一个包含 span 和 match 的对象
match = re.search('first', txt, re.I)
print(match)  # <re.Match object; span=(100, 105), match='first'>
# 我们可以使用 span 获取匹配的起始和结束位置，以元组形式返回
span = match.span()
print(span)     # (100, 105)
# 让我们从 span 中查找起始和结束位置
start, end = span
print(start, end)  # 100 105
substring = txt[start:end]
print(substring)       # first
```

正如你所见，search 比 match 好得多，因为它可以在整个文本中查找模式。Search 返回找到的第一个匹配项的匹配对象，否则返回 *None*。一个更好的 *re* 函数是 *findall*。该函数会检查整个字符串中的模式，并返回所有匹配项作为列表。

#### 使用 *findall* 搜索所有匹配项

*findall()* 返回所有匹配项作为列表

```py
txt = '''Python is the most beautiful language that a human being has ever created.
I recommend python for a first programming language'''

# 它返回一个列表
matches = re.findall('language', txt, re.I)
print(matches)  # ['language', 'language']
```

正如你所见，单词 *language* 在字符串中出现了两次。让我们再练习一下。
现在我们来查找字符串中的 Python 和 python 两个单词：

```py
txt = '''Python is the most beautiful language that a human being has ever created.
I recommend python for a first programming language'''

# 它返回列表
matches = re.findall('python', txt, re.I)
print(matches)  # ['Python', 'python']

```

由于我们使用了 *re.I*，因此包含了大写和小写字母。如果我们没有 re.I 标志，那么我们就必须以不同的方式编写模式。让我们来看看：

```py
txt = '''Python is the most beautiful language that a human being has ever created.
I recommend python for a first programming language'''

matches = re.findall('Python|python', txt)
print(matches)  # ['Python', 'python']

#
matches = re.findall('[Pp]ython', txt)
print(matches)  # ['Python', 'python']

```

#### 替换子字符串

```py
txt = '''Python is the most beautiful language that a human being has ever created.
I recommend python for a first programming language'''

match_replaced = re.sub('Python|python', 'JavaScript', txt, re.I)
print(match_replaced)  # JavaScript is the most beautiful language that a human being has ever created.I recommend python for a first programming language
# 或者（OR）
match_replaced = re.sub('[Pp]ython', 'JavaScript', txt, re.I)
print(match_replaced)  # JavaScript is the most beautiful language that a human being has ever created.I recommend python for a first programming language
```

让我们再添加一个示例。除非我们移除 % 符号，否则下面的字符串真的很难阅读。将 % 替换为空字符串将清理文本。

```py

txt = '''%I a%m te%%a%%che%r% a%n%d %% I l%o%ve te%ach%ing.
T%he%re i%s n%o%th%ing as r%ewarding a%s e%duc%at%i%ng a%n%d e%m%p%ow%er%ing p%e%o%ple.
I fo%und te%a%ching m%ore i%n%t%er%%es%ting t%h%an any other %jobs.
D%o%es thi%s m%ot%iv%a%te %y%o%u to b%e a t%e%a%cher?'''

matches = re.sub('%', '', txt)
print(matches)
```

```sh
I am teacher and I love teaching.
There is nothing as rewarding as educating and empowering people.
I found teaching more interesting than any other jobs. Does this motivate you to be a teacher?
```

## 使用 RegEx Split 分割文本

```py
txt = '''I am teacher and  I love teaching.
There is nothing as rewarding as educating and empowering people.
I found teaching more interesting than any other jobs.
Does this motivate you to be a teacher?'''
print(re.split('\n', txt)) # 使用 \n 分割 - 行尾符号
```

```sh
['I am teacher and  I love teaching.', 'There is nothing as rewarding as educating and empowering people.', 'I found teaching more interesting than any other jobs.', 'Does this motivate you to be a teacher?']
```

## 编写 RegEx 模式

要声明字符串变量，我们使用单引号或双引号。要声明 RegEx 变量，使用 *r''*。
以下模式仅识别小写的 apple，要使其不区分大小写，我们应该重写模式或添加标志。

```py
import re

regex_pattern = r'apple'
txt = 'Apple and banana are fruits. An old cliche says an apple a day a doctor way has been replaced by a banana a day keeps the doctor far far away. '
matches = re.findall(regex_pattern, txt)
print(matches)  # ['apple']

# 添加标志使其不区分大小写
matches = re.findall(regex_pattern, txt, re.I)
print(matches)  # ['Apple', 'apple']
# 或者我们可以使用字符集方法
regex_pattern = r'[Aa]pple'  # 这意味着首字母可以是 A 或 a
matches = re.findall(regex_pattern, txt)
print(matches)  # ['Apple', 'apple']

```

* []: 字符集
  - [a-c] 表示 a 或 b 或 c
  - [a-z] 表示从 a 到 z 的任意字母
  - [A-Z] 表示从 A 到 Z 的任意字符
  - [0-3] 表示 0 或 1 或 2 或 3
  - [0-9] 表示从 0 到 9 的任意数字
  - [A-Za-z0-9] 任意单个字符，即 a 到 z、A 到 Z 或 0 到 9
- \\: 用于转义特殊字符
  - \d 表示：匹配字符串中包含数字的位置（0-9）
  - \D 表示：匹配字符串中不包含数字的位置
- . : 除换行符（\n）外的任意字符
- ^: 以...开头
  - r'^substring' 例如 r'^love'，以单词 love 开头的句子
  - r'[^abc] 表示不是 a、不是 b、不是 c
- $: 以...结尾
  - r'substring$' 例如 r'love$'，以单词 love 结尾的句子
- *: 零次或多次
  - r'[a]*' 表示 a 可选或可以出现多次
- +: 一次或多次
  - r'[a]+' 表示至少一次（或更多）
- ?: 零次或一次
  - r'[a]?' 表示零次或一次
- {3}: 恰好 3 个字符
- {3,}: 至少 3 个字符
- {3,8}: 3 到 8 个字符
- |: 要么...要么...
  - r'apple|banana' 表示 apple 或 banana
- (): 捕获和分组

![Regular Expression cheat sheet](../images/regex.png)

让我们用示例来阐明上面的元字符（meta character）

### 方括号

让我们使用方括号来包含大写和小写

```py
regex_pattern = r'[Aa]pple' # 这个方括号表示 A 或 a
txt = 'Apple and banana are fruits. An old cliche says an apple a day a doctor way has been replaced by a banana a day keeps the doctor far far away.'
matches = re.findall(regex_pattern, txt)
print(matches)  # ['Apple', 'apple']
```

如果我们想查找 banana，我们将模式写成如下：

```py
regex_pattern = r'[Aa]pple|[Bb]anana' # 这个方括号表示 A 或 a
txt = 'Apple and banana are fruits. An old cliche says an apple a day a doctor way has been replaced by a banana a day keeps the doctor far far away.'
matches = re.findall(regex_pattern, txt)
print(matches)  # ['Apple', 'banana', 'apple', 'banana']
```

使用方括号和我们成功提取了 Apple、apple、Banana 和 banana。

### RegEx 中的转义字符（\\）

```py
regex_pattern = r'\d'  # d 是表示数字的特殊字符
txt = 'This regular expression example was made on December 6,  2019 and revised on July 8, 2021'
matches = re.findall(regex_pattern, txt)
print(matches)  # ['6', '2', '0', '1', '9', '8', '2', '0', '2', '1'], 这不是我们想要的
```

### 一次或多次（+）

```py
regex_pattern = r'\d+'  # d 是表示数字的特殊字符，+ 表示一次或多次
txt = 'This regular expression example was made on December 6,  2019 and revised on July 8, 2021'
matches = re.findall(regex_pattern, txt)
print(matches)  # ['6', '2019', '8', '2021'] - 现在好多了！
```

### 句号（.）

```py
regex_pattern = r'[a].'  # 这个方括号表示 a，. 表示除换行符外的任意字符
txt = '''Apple and banana are fruits'''
matches = re.findall(regex_pattern, txt)
print(matches)  # ['an', 'an', 'an', 'a ', 'ar']

regex_pattern = r'[a].+'  # . 任意字符，+ 任意字符一次或多次
matches = re.findall(regex_pattern, txt)
print(matches)  # ['and banana are fruits']
```

### 零次或多次（\*）

零次或多次。模式可能不出现，也可能出现多次。

```py
regex_pattern = r'[a].*'  # . 任意字符，* 任意字符零次或多次
txt = '''Apple and banana are fruits'''
matches = re.findall(regex_pattern, txt)
print(matches)  # ['and banana are fruits']
```

### 零次或一次（?）

零次或一次。模式可能不出现，也可能出现一次。

```py
txt = '''I am not sure if there is a convention how to write the word e-mail.
Some people write it as email others may write it as Email or E-mail.'''
regex_pattern = r'[Ee]-?mail'  # ? 表示这里的 '-' 是可选的
matches = re.findall(regex_pattern, txt)
print(matches)  # ['e-mail', 'email', 'Email', 'E-mail']
```

### RegEx 中的量词

我们可以使用花括号指定要查找的子字符串的长度。假设我们对长度为 4 个字符的子字符串感兴趣：

```py
txt = 'This regular expression example was made on December 6,  2019 and revised on July 8, 2021'
regex_pattern = r'\d{4}'  # 恰好四次
matches = re.findall(regex_pattern, txt)
print(matches)  # ['2019', '2021']

txt = 'This regular expression example was made on December 6,  2019 and revised on July 8, 2021'
regex_pattern = r'\d{1,4}'
matches = re.findall(regex_pattern, txt)
print(matches)  # ['6', '2019', '8', '2021']
```

### 脱字符 ^

- 以...开头

```py
txt = 'This regular expression example was made on December 6,  2019 and revised on July 8, 2021'
regex_pattern = r'^This'  # ^ 表示以...开头
matches = re.findall(regex_pattern, txt)
print(matches)  # ['This']
```

- 否定（Negation）

```py
txt = 'This regular expression example was made on December 6,  2019 and revised on July 8, 2021'
regex_pattern = r'[^A-Za-z ]+'  # ^ 在字符集中表示否定，不是 A 到 Z，不是 a 到 z，不是空格
matches = re.findall(regex_pattern, txt)
print(matches)  # ['6,', '2019', '8', '2021']
```

## 💻 练习 - 第 18 天

### 练习：第 1 级

 1. 以下段落中出现频率最高的单词是什么？

```py
    paragraph = 'I love teaching. If you do not love teaching what else can you love. I love Python if you do not love something which can give you all the capabilities to develop an application what else can you love.
```

```sh
    [
    (6, 'love'),
    (5, 'you'),
    (3, 'can'),
    (2, 'what'),
    (2, 'teaching'),
    (2, 'not'),
    (2, 'else'),
    (2, 'do'),
    (2, 'I'),
    (1, 'which'),
    (1, 'to'),
    (1, 'the'),
    (1, 'something'),
    (1, 'if'),
    (1, 'give'),
    (1, 'develop'),
    (1, 'capabilities'),
    (1, 'application'),
    (1, 'an'),
    (1, 'all'),
    (1, 'Python'),
    (1, 'If')
    ]
```

2. 水平 x 轴上某些粒子的位置为：负方向上的 -12、-4、-3 和 -1，原点处的 0，正方向上的 4 和 8。从这段文本中提取这些数字，并找出两个最远粒子之间的距离。

```py
points = ['-12', '-4', '-3', '-1', '0', '4', '8']
sorted_points =  [-12, -4, -3, -1, -1, 0, 2, 4, 8]
distance = 8 -(-12) # 20
```

### 练习：第 2 级

1. 编写一个模式，用于判断字符串是否是有效的 Python 变量

    ```sh
    is_valid_variable('first_name') # True
    is_valid_variable('first-name') # False
    is_valid_variable('1first_name') # False
    is_valid_variable('firstname') # True
    ```

### 练习：第 3 级

1. 清理以下文本。清理后，统计字符串中出现频率最高的三个单词。

    ```py
    sentence = '''%I $am@% a %tea@cher%, &and& I lo%#ve %tea@ching%;. There $is nothing; &as& mo@re rewarding as educa@ting &and& @emp%o@wering peo@ple. ;I found tea@ching m%o@re interesting tha@n any other %jo@bs. %Do@es thi%s mo@tivate yo@u to be a tea@cher!?'''

    print(clean_text(sentence));
    I am a teacher and I love teaching There is nothing as more rewarding as educating and empowering people I found teaching more interesting than any other jobs Does this motivate you to be a teacher
    print(most_frequent_words(cleaned_text)) # [(3, 'I'), (2, 'teaching'), (2, 'teacher')]
    ```

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 17 天](../17_Day_Exception_handling/17_exception_handling_异常处理.md) | [第 19 天 >>](../19_Day_File_handling/19_file_handling_文件处理.md)
