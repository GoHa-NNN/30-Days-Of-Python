<div align="center">
  <h1> 🐍 30 Days Of Python：第 20 天 - PIP（Python 包管理器）</h1>
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

[<< 第 19 天](../19_Day_File_handling_文件处理/19_file_handling_文件处理.md) | [第 21 天 >>](../21_Day_Classes_and_objects_类与对象/21_classes_and_objects_类与对象.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 20 天](#-第-20-天)
  - [Python PIP - Python 包管理器](#python-pip---python-包管理器)
    - [什么是 PIP？](#什么是-pip)
    - [安装 PIP](#安装-pip)
    - [使用 pip 安装包](#使用-pip-安装包)
    - [卸载包](#卸载包)
    - [包列表](#包列表)
    - [显示包信息](#显示包信息)
    - [PIP Freeze](#pip-freeze)
    - [从 URL 读取](#从-url-读取)
    - [创建包](#创建包)
    - [关于包的更多信息](#关于包的更多信息)
  - [💻 练习 - 第 20 天](#-练习---第-20-天)

# 📘 第 20 天

## Python PIP - Python 包管理器

### 什么是 PIP？

PIP 代表首选安装程序（Preferred installer program）。我们使用 _pip_ 来安装不同的 Python 包（package）。
包是一个 Python 模块（module），可以包含一个或多个模块或其他包。我们可以安装到应用程序中的模块就是包。
在编程中，我们不必编写每一个实用程序，而是安装包并将它们导入到我们的应用程序中。

### 安装 PIP

如果你还没有安装 pip，让我们现在就安装它。打开你的终端（terminal）或命令提示符（command prompt）并复制粘贴以下内容：

```sh
asabeneh@Asabeneh:~$ pip install pip
```

通过以下命令检查 pip 是否已安装

```sh
pip --version
```

```py
asabeneh@Asabeneh:~$ pip --version
pip 21.1.3 from /usr/local/lib/python3.7/site-packages/pip (python 3.9.6)
```

正如你所见，我使用的是 pip 版本 21.1.3，如果你看到的数字略低于或高于此值，说明你已经安装了 pip。

让我们看看 Python 社区中用于不同目的的一些包。只是为了让你知道，有大量可用于不同应用程序的包。

### 使用 pip 安装包

让我们尝试安装 _numpy_，即 numeric Python。它是机器学习和数据科学社区中最受欢迎的包之一。

- NumPy 是 Python 科学计算的基础包。它包含以下内容：
  - 一个强大的 N 维数组对象
  - 复杂的（广播）函数
  - 用于集成 C/C++ 和 Fortran 代码的工具
  - 实用的线性代数、傅里叶变换和随机数功能

```sh
asabeneh@Asabeneh:~$ pip install numpy
```

让我们开始使用 numpy。打开你的 Python 交互式解释器（interactive shell），输入 python，然后按如下方式导入 numpy：

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy
>>> numpy.version.version
'1.20.1'
>>> lst = [1, 2, 3,4, 5]
>>> np_arr = numpy.array(lst)
>>> np_arr
array([1, 2, 3, 4, 5])
>>> len(np_arr)
5
>>> np_arr * 2
array([ 2,  4,  6,  8, 10])
>>> np_arr  + 2
array([3, 4, 5, 6, 7])
>>>
```

Pandas 是一个开源的 BSD 许可库，为 Python 编程语言提供高性能、易于使用的数据结构和数据分析工具。让我们安装 numpy 的大哥——_pandas_：

```sh
asabeneh@Asabeneh:~$ pip install pandas
```

```py
asabeneh@Asabeneh:~$ python
Python 3.9.6 (default, Jun 28 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import pandas
```

本节不是关于 numpy 或 pandas 的，在这里我们试图学习如何安装包以及如何导入它们。如果需要，我们将在其他章节中讨论不同的包。

让我们导入一个网页浏览器模块，它可以帮助我们打开任何网站。我们不需要安装这个模块，它已经随 Python 3 默认安装。例如，如果你想随时打开任意数量的网站，或者如果你想安排某些事情，可以使用这个 _webbrowser_ 模块。

```py
import webbrowser # 用于打开网站的网页浏览器模块

# url 列表：python
url_lists = [
    'http://www.python.org',
    'https://www.linkedin.com/in/asabeneh/',
    'https://github.com/Asabeneh',
    'https://twitter.com/Asabeneh',
]

# 在不同的标签页中打开上述网站列表
for url in url_lists:
    webbrowser.open_new_tab(url)
```

### 卸载包

如果你不想保留已安装的包，可以使用以下命令删除它们。

```sh
pip uninstall packagename
```

### 包列表

查看我们机器上已安装的包。我们可以使用 pip 后跟 list。

```sh
pip list
```

### 显示包信息

显示有关包的信息

```sh
pip show packagename
```

```sh
asabeneh@Asabeneh:~$ pip show pandas
Name: pandas
Version: 1.2.3
Summary: Powerful data structures for data analysis, time series, and statistics
Home-page: http://pandas.pydata.org
Author: None
Author-email: None
License: BSD
Location: /usr/local/lib/python3.7/site-packages
Requires: python-dateutil, pytz, numpy
Required-by:
```

如果我们想要更多细节，只需添加 --verbose

```sh
asabeneh@Asabeneh:~$ pip show --verbose pandas
Name: pandas
Version: 1.2.3
Summary: Powerful data structures for data analysis, time series, and statistics
Home-page: http://pandas.pydata.org
Author: None
Author-email: None
License: BSD
Location: /usr/local/lib/python3.7/site-packages
Requires: numpy, pytz, python-dateutil
Required-by:
Metadata-Version: 2.1
Installer: pip
Classifiers:
  Development Status :: 5 - Production/Stable
  Environment :: Console
  Operating System :: OS Independent
  Intended Audience :: Science/Research
  Programming Language :: Python
  Programming Language :: Python :: 3
  Programming Language :: Python :: 3.5
  Programming Language :: Python :: 3.6
  Programming Language :: Python :: 3.7
  Programming Language :: Python :: 3.8
  Programming Language :: Cython
  Topic :: Scientific/Engineering
Entry-points:
  [pandas_plotting_backends]
  matplotlib = pandas:plotting._matplotlib
```

### PIP Freeze

生成已安装的 Python 包及其版本，输出适合在 requirements 文件中使用。requirements.txt 文件是一个包含 Python 项目中所有已安装 Python 包的文件。

```sh
asabeneh@Asabeneh:~$ pip freeze
docutils==0.11
Jinja2==2.7.2
MarkupSafe==0.19
Pygments==1.6
Sphinx==1.2.2
```

pip freeze 为我们提供了已使用和安装的包及其版本。我们将其与 requirements.txt 文件一起用于部署。

### 从 URL 读取

到目前为止，你已经熟悉了如何读取或写入本地机器上的文件。有时，我们想使用 URL 从网站读取数据或从 API 读取数据。
API 代表应用程序编程接口（Application Program Interface）。它是服务器之间交换结构化数据的一种方式，主要以 JSON 数据形式。要打开网络连接，我们需要一个名为 _requests_ 的包——它允许打开网络连接并实现 CRUD（create, read, update and delete）操作。在本节中，我们仅涵盖 CRUD 中的读取或获取部分。

让我们安装 _requests_：

```py
asabeneh@Asabeneh:~$ pip install requests
```

我们将在 _requests_ 模块中看到 _get_、_status_code_、_headers_、_text_ 和 _json_ 方法：
  - _get()_: 打开网络并从 URL 获取数据——它返回一个响应对象
  - _status_code_: 获取数据后，我们可以检查操作的状态（成功、错误等）
  - _headers_: 检查标头类型
  - _text_: 从获取的响应对象中提取文本
  - _json_: 提取 JSON 数据
让我们从这个网站读取一个 txt 文件，https://www.w3.org/TR/PNG/iso_8859-1.txt。

```py
import requests # 导入 request 模块

url = 'https://www.w3.org/TR/PNG/iso_8859-1.txt' # 来自网站的文本

response = requests.get(url) # 打开网络并获取数据
print(response)
print(response.status_code) # 状态码，成功：200
print(response.headers)     # 标头信息
print(response.text) # 给出页面中的所有文本
```

```sh
<Response [200]>
200
{'date': 'Sun, 08 Dec 2019 18:00:31 GMT', 'last-modified': 'Fri, 07 Nov 2003 05:51:11 GMT', 'etag': '"17e9-3cb82080711c0;50c0b26855880-gzip"', 'accept-ranges': 'bytes', 'cache-control': 'max-age=31536000', 'expires': 'Mon, 07 Dec 2020 18:00:31 GMT', 'vary': 'Accept-Encoding', 'content-encoding': 'gzip', 'access-control-allow-origin': '*', 'content-length': '1616', 'content-type': 'text/plain', 'strict-transport-security': 'max-age=15552000; includeSubdomains; preload', 'content-security-policy': 'upgrade-insecure-requests'}
```

- 让我们从 API 读取数据。API 代表应用程序编程接口。它是服务器之间交换结构化数据的一种方式，主要是 JSON 数据。一个 API 示例：https://restcountries.eu/rest/v2/all。让我们使用 _requests_ 模块读取这个 API。

```py
import requests
url = 'https://restcountries.eu/rest/v2/all'  # 国家 api
response = requests.get(url)  # 打开网络并获取数据
print(response) # 响应对象
print(response.status_code)  # 状态码，成功：200
countries = response.json()
print(countries[:1])  # 我们只切片了第一个国家，移除切片以查看所有国家
```

```sh
<Response [200]>
200
[{'alpha2Code': 'AF',
  'alpha3Code': 'AFG',
  'altSpellings': ['AF', 'Afġānistān'],
  'area': 652230.0,
  'borders': ['IRN', 'PAK', 'TKM', 'UZB', 'TJK', 'CHN'],
  'callingCodes': ['93'],
  'capital': 'Kabul',
  'cioc': 'AFG',
  'currencies': [{'code': 'AFN', 'name': 'Afghan afghani', 'symbol': '؋'}],
  'demonym': 'Afghan',
  'flag': 'https://restcountries.eu/data/afg.svg',
  'gini': 27.8,
  'languages': [{'iso639_1': 'ps',
                 'iso639_2': 'pus',
                 'name': 'Pashto',
                 'nativeName': 'پښتو'},
                {'iso639_1': 'uz',
                 'iso639_2': 'uzb',
                 'name': 'Uzbek',
                 'nativeName': 'Oʻzbek'},
                {'iso639_1': 'tk',
                 'iso639_2': 'tuk',
                 'name': 'Turkmen',
                 'nativeName': 'Türkmen'}],
  'latlng': [33.0, 65.0],
  'name': 'Afghanistan',
  'nativeName': 'افغانستان',
  'numericCode': '004',
  'population': 27657145,
  'region': 'Asia',
  'regionalBlocs': [{'acronym': 'SAARC',
                     'name': 'South Asian Association for Regional Cooperation',
                     'otherAcronyms': [],
                     'otherNames': []}],
  'subregion': 'Southern Asia',
  'timezones': ['UTC+04:30'],
  'topLevelDomain': ['.af'],
  'translations': {'br': 'Afeganistão',
                   'de': 'Afghanistan',
                   'es': 'Afganistán',
                   'fa': 'افغانستان',
                   'fr': 'Afghanistan',
                   'hr': 'Afganistan',
                   'it': 'Afghanistan',
                   'ja': 'アフガニスタン',
                   'nl': 'Afghanistan',
                   'pt': 'Afeganistão'}}]
```

如果我们获取的是 JSON 数据，则使用响应对象中的 _json()_ 方法。对于 txt、html、xml 和其他文件格式，我们可以使用 _text_。

### 创建包

我们根据某些标准将大量文件组织在不同的文件夹和子文件夹中，以便我们能够轻松找到和管理它们。如你所知，一个模块可以包含多个对象，如类、函数等。一个包可以包含一个或多个相关模块。包实际上是一个包含一个或多个模块文件的文件夹。让我们按照以下步骤创建一个名为 mypackage 的包：

在 30DaysOfPython 文件夹内创建一个名为 mypackage 的新文件夹
在 mypackage 文件夹中创建一个空的 **__init__**.py 文件。
使用以下代码创建模块 arithmetic.py 和 greet.py：

```py
# mypackage/arithmetics.py
# arithmetics.py
def add_numbers(*args):
    total = 0
    for num in args:
        total += num
    return total


def subtract(a, b):
    return (a - b)


def multiple(a, b):
    return a * b


def division(a, b):
    return a / b


def remainder(a, b):
    return a % b


def power(a, b):
    return a ** b
```

```py
# mypackage/greet.py
# greet.py
def greet_person(firstname, lastname):
    return f'{firstname} {lastname}, welcome to 30DaysOfPython Challenge!'
```

你的包的文件夹结构应该如下所示：

```sh
─ mypackage
    ├── __init__.py
    ├── arithmetic.py
    └── greet.py
```

现在让我们打开 Python 交互式解释器并尝试我们创建的包：

```sh
asabeneh@Asabeneh:~/Desktop/30DaysOfPython$ python
Python 3.9.6 (default, Jun 28, 2021, 15:26:21)
[Clang 11.0.0 (clang-1100.0.33.8)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> from mypackage import arithmetics
>>> arithmetics.add_numbers(1, 2, 3, 5)
11
>>> arithmetics.subtract(5, 3)
2
>>> arithmetics.multiple(5, 3)
15
>>> arithmetics.division(5, 3)
1.6666666666666667
>>> arithmetics.remainder(5, 3)
2
>>> arithmetics.power(5, 3)
125
>>> from mypackage import greet
>>> greet.greet_person('Asabeneh', 'Yetayeh')
'Asabeneh Yetayeh, welcome to 30DaysOfPython Challenge!'
>>>
```

正如你所见，我们的包运行完美。包文件夹包含一个名为 **__init__**.py 的特殊文件——它存储包的内容。如果我们将 **__init__**.py 放在包文件夹中，Python 就会开始将其识别为包。
**__init__**.py 将其模块中的指定资源暴露出来，以便导入到其他 Python 文件中。当导入包时，空的 **__init__**.py 文件使所有函数可用。**__init__**.py 对于文件夹被 Python 识别为包至关重要。

### 关于包的更多信息

- 数据库（Database）
  - SQLAlchemy 或 SQLObject - 面向对象的多种不同数据库系统访问
    - _pip install SQLAlchemy_
- Web 开发（Web Development）
  - Django - 高级 Web 框架。
    - _pip install django_
  - Flask - 基于 Werkzeug、Jinja 2 的 Python 微框架。（BSD 许可）
    - _pip install flask_
- HTML 解析器（HTML Parser）
  - [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/) - 专为快速周转项目（如屏幕抓取）设计的 HTML/XML 解析器，可接受不良标记。
    - _pip install beautifulsoup4_
  - PyQuery - 在 Python 中实现 jQuery；显然比 BeautifulSoup 更快。

- XML 处理（XML Processing）
  - ElementTree - Element 类型是一个简单但灵活的容器对象，设计用于在内存中存储层次数据结构，如简化的 XML 信息集。——注意：Python 2.5 及以上版本在标准库中包含 ElementTree
- GUI
  - PyQt - 跨平台 Qt 框架的绑定。
  - TkInter - 传统的 Python 用户界面工具包。
- 数据分析、数据科学和机器学习（Data Analysis, Data Science and Machine learning）
  - Numpy：Numpy（numeric Python）被认为是 Python 中最受欢迎的机器学习库之一。
  - Pandas：是一个 Python 数据分析、数据科学和机器学习库，提供高级数据结构和各种分析工具。
  - SciPy：SciPy 是面向应用程序开发人员和工程师的机器学习库。SciPy 库包含用于优化、线性代数、积分、图像处理和统计的模块。
  - Scikit-Learn：它是 NumPy 和 SciPy。它被认为是处理复杂数据的最佳库之一。
  - TensorFlow：是 Google 构建的机器学习库。
  - Keras：被认为是 Python 中最酷的机器学习库之一。它提供了一种更简单的机制来表达神经网络。Keras 还提供了一些用于编译模型、处理数据集、可视化图表等的最佳实用工具。
- 网络（Network）：
  - requests：是一个我们可以用来向服务器发送请求的包（GET、POST、DELETE、PUT）
    - _pip install requests_

🌕 你一直在进步，在通往伟大的道路上已经领先了 20 步。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 20 天

1. 读取此 URL 并找出出现频率最高的 10 个单词。romeo_and_juliet = 'http://www.gutenberg.org/files/1112/1112.txt'
2. 读取 cats API 和 cats_api = 'https://api.thecatapi.com/v1/breeds' 并找出：
   1. 以公制单位表示的猫体重的最小值、最大值、均值、中位数、标准差。
   2. 以年为单位的猫寿命的最小值、最大值、均值、中位数、标准差。
   3. 创建猫的国家与品种的频率表。
3. 读取[国家 API](https://restcountries.eu/rest/v2/all)并找出
   1. 10 个最大的国家
   2. 10 种使用人数最多的语言
   3. 国家 API 中语言的总数
4. UCI 是获取数据科学和机器学习数据集的最常见场所之一。读取 UCL 的内容（https://archive.ics.uci.edu/ml/datasets.php）。没有额外的库会很困难，所以你可以尝试使用 BeautifulSoup4。

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 19 天](../19_Day_File_handling_文件处理/19_file_handling_文件处理.md) | [第 21 天 >>](../21_Day_Classes_and_objects_类与对象/21_classes_and_objects_类与对象.md)
