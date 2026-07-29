<div align="center">
  <h1> 🐍 30 Days Of Python：第 19 天 - 文件处理（File Handling）</h1>
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

[<< 第 18 天](../18_Day_Regular_expressions_正则表达式/18_regular_expressions_正则表达式.md) | [第 20 天 >>](../20_Day_Python_package_manager_包管理器/20_python_package_manager_Python包管理器.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 19 天](#-第-19-天)
  - [文件处理](#文件处理)
    - [打开文件进行读取](#打开文件进行读取)
    - [打开文件进行写入和更新](#打开文件进行写入和更新)
    - [删除文件](#删除文件)
  - [文件类型](#文件类型)
    - [带 txt 扩展名的文件](#带-txt-扩展名的文件)
    - [带 json 扩展名的文件](#带-json-扩展名的文件)
    - [将 JSON 转换为字典](#将-json-转换为字典)
    - [将字典转换为 JSON](#将字典转换为-json)
    - [保存为 JSON 文件](#保存为-json-文件)
    - [带 csv 扩展名的文件](#带-csv-扩展名的文件)
    - [带 xlsx 扩展名的文件](#带-xlsx-扩展名的文件)
    - [带 xml 扩展名的文件](#带-xml-扩展名的文件)
  - [💻 练习 - 第 19 天](#-练习---第-19-天)
    - [练习：第 1 级](#练习第-1-级)
    - [练习：第 2 级](#练习第-2-级)
    - [练习：第 3 级](#练习第-3-级)

# 📘 第 19 天

## 文件处理

到目前为止，我们已经了解了不同的 Python 数据类型。我们通常将数据存储在不同的文件格式中。除了处理文件外，我们还将在本节中看到不同的文件格式（.txt、.json、.xml、.csv、.tsv、.excel）。首先，让我们熟悉使用常见文件格式（.txt）处理文件。

文件处理是编程的重要组成部分，它允许我们创建、读取、更新和删除文件。在 Python 中，我们使用 _open()_ 内置函数来处理数据。

```py
# 语法
open('filename', mode) # mode(r, a, w, x, t,b) 可以是读取、写入、更新
```

- "r" - 读取（Read） - 默认值。打开文件进行读取，如果文件不存在则返回错误
- "a" - 追加（Append） - 打开文件进行追加，如果文件不存在则创建文件
- "w" - 写入（Write） - 打开文件进行写入，如果文件不存在则创建文件
- "x" - 创建（Create） - 创建指定的文件，如果文件存在则返回错误
- "t" - 文本（Text） - 默认值。文本模式
- "b" - 二进制（Binary） - 二进制模式（例如图像）

### 打开文件进行读取

_open_ 的默认模式是读取，因此我们不必指定 'r' 或 'rt'。我已经在 files 目录中创建并保存了一个名为 reading_file_example.txt 的文件。让我们看看它是如何完成的：

```py
f = open('./files/reading_file_example.txt')
print(f) # <_io.TextIOWrapper name='./files/reading_file_example.txt' mode='r' encoding='UTF-8'>
```

从上面的示例中可以看到，我打印了打开的文件，它提供了一些相关信息。打开的文件有不同的读取方法：_read()_、_readline_、_readlines_。打开的文件必须使用 _close()_ 方法关闭。

- _read()_: 将整个文本作为字符串读取。如果我们想限制要读取的字符数，可以通过向 *read(number)* 方法传递 int 值来限制。

```py
f = open('./files/reading_file_example.txt')
txt = f.read()
print(type(txt))
print(txt)
f.close()
```

```sh
# 输出
<class 'str'>
This is an example to show how to open a file and read.
This is the second line of the text.
```

让我们不打印所有文本，而是打印文本文件的前 10 个字符。

```py
f = open('./files/reading_file_example.txt')
txt = f.read(10)
print(type(txt))
print(txt)
f.close()
```

```sh
# 输出
<class 'str'>
This is an
```

- _readline()_: 仅读取第一行

```py
f = open('./files/reading_file_example.txt')
line = f.readline()
print(type(line))
print(line)
f.close()
```

```sh
# 输出
<class 'str'>
This is an example to show how to open a file and read.
```

- _readlines()_: 逐行读取所有文本并返回行的列表

```py
f = open('./files/reading_file_example.txt')
lines = f.readlines()
print(type(lines))
print(lines)
f.close()
```

```sh
# 输出
<class 'list'>
['This is an example to show how to open a file and read.\n', 'This is the second line of the text.']
```

获取所有行的另一种方法是使用 _splitlines()_：

```py
f = open('./files/reading_file_example.txt')
lines = f.read().splitlines()
print(type(lines))
print(lines)
f.close()
```

```sh
# 输出
<class 'list'>
['This is an example to show how to open a file and read.', 'This is the second line of the text.']
```

在我们打开文件后，应该关闭它们。人们很容易忘记关闭文件。有一种使用 _with_ 打开文件的新方法——它会自动关闭文件。让我们用 _with_ 方法重写前面的示例：

```py
with open('./files/reading_file_example.txt') as f:
    lines = f.read().splitlines()
    print(type(lines))
    print(lines)
```

```sh
# 输出
<class 'list'>
['This is an example to show how to open a file and read.', 'This is the second line of the text.']
```

### 打开文件进行写入和更新

要向现有文件写入内容，我们必须向 _open()_ 函数添加一个模式参数：

- "a" - 追加 - 将追加到文件末尾，如果文件不存在则创建新文件。
- "w" - 写入 - 将覆盖任何现有内容，如果文件不存在则创建。

让我们向一直在读取的文件追加一些文本：

```py
with open('./files/reading_file_example.txt','a') as f:
    f.write('This text has to be appended at the end')
```

如果文件不存在，以下方法会创建一个新文件：

```py
with open('./files/writing_file_example.txt','w') as f:
    f.write('This text will be written in a newly created file')
```

### 删除文件

我们已经在上一节中了解了如何使用 _os_ 模块创建和删除目录。同样，如果我们想删除文件，需要使用 _os_ 模块。

```py
import os
os.remove('./files/example.txt')

```

如果文件不存在，remove 方法将抛出错误，因此最好使用如下条件：

```py
import os
if os.path.exists('./files/example.txt'):
    os.remove('./files/example.txt')
else:
    print('The file does not exist')
```

## 文件类型

### 带 txt 扩展名的文件

带 _txt_ 扩展名的文件是一种非常常见的数据形式，我们已经在上一节中介绍过。让我们转向 JSON 文件。

### 带 json 扩展名的文件

JSON 代表 JavaScript 对象表示法（JavaScript Object Notation）。实际上，它是一个字符串化的 JavaScript 对象或 Python 字典。

_示例：_

```py
# 字典
person_dct= {
    "name":"Asabeneh",
    "country":"Finland",
    "city":"Helsinki",
    "skills":["JavaScrip", "React","Python"]
}
# JSON：字典的字符串形式
person_json = "{'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'skills': ['JavaScrip', 'React', 'Python']}"

# 我们使用三引号并使其成为多行以提高可读性
person_json = '''{
    "name":"Asabeneh",
    "country":"Finland",
    "city":"Helsinki",
    "skills":["JavaScrip", "React","Python"]
}'''
```

### 将 JSON 转换为字典

要将 JSON 转换为字典，首先我们导入 json 模块，然后使用 _loads_ 方法。

```py
import json
# JSON
person_json = '''{
    "name": "Asabeneh",
    "country": "Finland",
    "city": "Helsinki",
    "skills": ["JavaScrip", "React", "Python"]
}'''
# 让我们将 JSON 转换为字典
person_dct = json.loads(person_json)
print(type(person_dct))
print(person_dct)
print(person_dct['name'])
```

```sh
# 输出
<class 'dict'>
{'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'skills': ['JavaScrip', 'React', 'Python']}
Asabeneh
```

### 将字典转换为 JSON

要将字典转换为 JSON，我们使用 json 模块中的 _dumps_ 方法。

```py
import json
# Python 字典
person = {
    "name": "Asabeneh",
    "country": "Finland",
    "city": "Helsinki",
    "skills": ["JavaScrip", "React", "Python"]
}
# 让我们将其转换为 json
person_json = json.dumps(person, indent=4) # indent 可以是 2、4、8。它美化了 json
print(type(person_json))
print(person_json)
```

```sh
# 输出
# 当你打印它时，它没有引号，但实际上它是一个字符串
# JSON 没有类型，它是字符串类型。
<class 'str'>
{
    "name": "Asabeneh",
    "country": "Finland",
    "city": "Helsinki",
    "skills": [
        "JavaScrip",
        "React",
        "Python"
    ]
}
```

### 保存为 JSON 文件

我们还可以将数据保存为 json 文件。让我们使用以下步骤将其保存为 json 文件。要写入 json 文件，我们使用 json.dump() 方法，它可以接受字典、输出文件、ensure_ascii 和 indent。

```py
import json
# Python 字典
person = {
    "name": "Asabeneh",
    "country": "Finland",
    "city": "Helsinki",
    "skills": ["JavaScrip", "React", "Python"]
}
with open('./files/json_example.json', 'w', encoding='utf-8') as f:
    json.dump(person, f, ensure_ascii=False, indent=4)
```

在上面的代码中，我们使用了编码（encoding）和缩进（indentation）。缩进使 json 文件易于阅读。

### 带 csv 扩展名的文件

CSV 代表逗号分隔值（comma separated values）。CSV 是一种简单的文件格式，用于存储表格数据，如电子表格或数据库。CSV 是数据科学中非常常见的数据格式。

**示例：**

```csv
"name","country","city","skills"
"Asabeneh","Finland","Helsinki","JavaScript"
```

**示例：**

```py
import csv
with open('./files/csv_example.csv') as f:
    csv_reader = csv.reader(f, delimiter=',') # 我们使用 reader 方法读取 csv
    line_count = 0
    for row in csv_reader:
        if line_count == 0:
            print(f'Column names are :{", ".join(row)}')
            line_count += 1
        else:
            print(
                f'\t{row[0]} is a teachers. He lives in {row[1]}, {row[2]}.')
            line_count += 1
    print(f'Number of lines:  {line_count}')
```

```sh
# 输出：
Column names are :name, country, city, skills
Number of lines:  1
        Asabeneh is a teacher. He lives in Finland, Helsinki.
Number of lines:  2
```

### 带 xlsx 扩展名的文件

要读取 Excel 文件，我们需要安装 _xlrd_ 包。我们将在介绍使用 pip 安装包之后再介绍这个。

```py
import xlrd
excel_book = xlrd.open_workbook('sample.xls')
print(excel_book.nsheets)
print(excel_book.sheet_names)
```

### 带 xml 扩展名的文件

XML 是另一种类似 HTML 的结构化数据格式。在 XML 中，标签不是预定义的。第一行是 XML 声明。person 标签是 XML 的根。person 有一个 gender 属性。
**示例：XML**

```xml
<?xml version="1.0"?>
<person gender="female">
  <name>Asabeneh</name>
  <country>Finland</country>
  <city>Helsinki</city>
  <skills>
    <skill>JavaScrip</skill>
    <skill>React</skill>
    <skill>Python</skill>
  </skills>
</person>
```

有关如何读取 XML 文件的更多信息，请查看[文档](https://docs.python.org/2/library/xml.etree.elementtree.html)

```py
import xml.etree.ElementTree as ET
tree = ET.parse('./files/xml_example.xml')
root = tree.getroot()
print('Root tag:', root.tag)
print('Attribute:', root.attrib)
for child in root:
    print('field: ', child.tag)
```

```sh
# 输出
Root tag: person
Attribute: {'gender': 'male'}
field: name
field: country
field: city
field: skills
```

🌕 你正在取得巨大进步。保持你的势头，继续努力。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 19 天

### 练习：第 1 级

1. 编写一个函数，用于计算文本中的行数和单词数。所有文件都在 data 文件夹中：
   1) 读取 obama_speech.txt 文件并计算行数和单词数
   2) 读取 michelle_obama_speech.txt 文件并计算行数和单词数
   3) 读取 donald_speech.txt 文件并计算行数和单词数
   4) 读取 melina_trump_speech.txt 文件并计算行数和单词数
2. 读取 data 目录中的 countries_data.json 数据文件，创建一个函数来找出使用人数最多的十种语言

   ```py
   # 你的输出应该像这样
   print(most_spoken_languages(filename='./data/countries_data.json', 10))
   [(91, 'English'),
   (45, 'French'),
   (25, 'Arabic'),
   (24, 'Spanish'),
   (9, 'Russian'),
   (9, 'Portuguese'),
   (8, 'Dutch'),
   (7, 'German'),
   (5, 'Chinese'),
   (4, 'Swahili'),
   (4, 'Serbian')]

   # 你的输出应该像这样
   print(most_spoken_languages(filename='./data/countries_data.json', 3))
   [(91, 'English'),
   (45, 'French'),
   (25, 'Arabic')]
   ```

3. 读取 data 目录中的 countries_data.json 数据文件，创建一个函数来创建人口最多的十个国家的列表

   ```py
   # 你的输出应该像这样
   print(most_populated_countries(filename='./data/countries_data.json', 10))

   [
   {'country': 'China', 'population': 1377422166},
   {'country': 'India', 'population': 1295210000},
   {'country': 'United States of America', 'population': 323947000},
   {'country': 'Indonesia', 'population': 258705000},
   {'country': 'Brazil', 'population': 206135893},
   {'country': 'Pakistan', 'population': 194125062},
   {'country': 'Nigeria', 'population': 186988000},
   {'country': 'Bangladesh', 'population': 161006790},
   {'country': 'Russian Federation', 'population': 146599183},
   {'country': 'Japan', 'population': 126960000}
   ]

   # 你的输出应该像这样

   print(most_populated_countries(filename='./data/countries_data.json', 3))
   [
   {'country': 'China', 'population': 1377422166},
   {'country': 'India', 'population': 1295210000},
   {'country': 'United States of America', 'population': 323947000}
   ]
   ```

### 练习：第 2 级

1. 从 email_exchange_big.txt 文件提取所有传入的电子邮件地址作为列表。
2. 找出英语中最常见的单词。将你的函数命名为 find_most_common_words，它将接受两个参数——一个字符串或文件和一个正整数，表示单词数量。你的函数将按降序返回一个元组数组。检查输出。

```py
    # 你的输出应该像这样
    print(find_most_common_words('sample.txt', 10))
    [(10, 'the'),
    (8, 'be'),
    (6, 'to'),
    (6, 'of'),
    (5, 'and'),
    (4, 'a'),
    (4, 'in'),
    (3, 'that'),
    (2, 'have'),
    (2, 'I')]

    # 你的输出应该像这样
    print(find_most_common_words('sample.txt', 5))

    [(10, 'the'),
    (8, 'be'),
    (6, 'to'),
    (6, 'of'),
    (5, 'and')]
```

3. 使用函数 find_most_frequent_words 来找出：
   1) [Obama 的演讲](https://github.com/Asabeneh/30-Days-Of-Python/blob/master/data/obama_speech.txt)中使用频率最高的十个单词
   2) [Michelle 的演讲](https://github.com/Asabeneh/30-Days-Of-Python/blob/master/data/michelle_obama_speech.txt)中使用频率最高的十个单词
   3) [Trump 的演讲](https://github.com/Asabeneh/30-Days-Of-Python/blob/master/data/donald_speech.txt)中使用频率最高的十个单词
   4) [Melina 的演讲](https://github.com/Asabeneh/30-Days-Of-Python/blob/master/data/melina_trump_speech.txt)中使用频率最高的十个单词
4. 编写一个 Python 应用程序来检查两个文本之间的相似度。它接受文件或字符串作为参数，并将评估两个文本的相似度。例如，检查[Michelle 的](https://github.com/Asabeneh/30-Days-Of-Python/blob/master/data/michelle_obama_speech.txt)和[Melina 的](https://github.com/Asabeneh/30-Days-Of-Python/blob/master/data/melina_trump_speech.txt)演讲文本之间的相似度。你可能需要几个函数：清理文本的函数（clean_text）、移除辅助词的函数（remove_support_words）以及最终检查相似度的函数（check_text_similarity）。[停用词](https://github.com/Asabeneh/30-Days-Of-Python/blob/master/data/stop_words.py)列表在 data 目录中。
5. 找出 romeo_and_juliet.txt 中重复次数最多的 10 个单词。
6. 阅读 [hacker news csv](https://github.com/Asabeneh/30-Days-Of-Python/blob/master/data/hacker_news.csv) 文件并找出：
   1) 计算包含 python 或 Python 的行数
   2) 计算包含 JavaScript、javascript 或 Javascript 的行数
   3) 计算包含 Java 但不包含 JavaScript 的行数

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 18 天](../18_Day_Regular_expressions_正则表达式/18_regular_expressions_正则表达式.md) | [第 20 天 >>](../20_Day_Python_package_manager_包管理器/20_python_package_manager_Python包管理器.md)
