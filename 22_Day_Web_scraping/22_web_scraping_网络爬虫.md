<div align="center">
  <h1> 🐍 30 Days Of Python：第 22 天 - 网络爬虫（Web Scraping）</h1>
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

[<< 第 21 天](../21_Day_Classes_and_objects/21_classes_and_objects_类与对象.md) | [第 23 天 >>](../23_Day_Virtual_environment/23_virtual_environment_虚拟环境.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 22 天](#-第-22-天)
  - [Python 网络爬虫](#python-网络爬虫)
    - [什么是网络爬虫](#什么是网络爬虫)
  - [💻 练习 - 第 22 天](#-练习---第-22-天)

# 📘 第 22 天

## Python 网络爬虫

### 什么是网络爬虫

互联网上充满了大量可用于不同目的的数据。要收集这些数据，我们需要知道如何从网站上抓取（scrape）数据。

网络爬虫（Web scraping）是从网站提取和收集数据，并将其存储在本地机器或数据库中的过程。

在本节中，我们将使用 beautifulsoup 和 requests 包来抓取数据。我们使用的包版本是 beautifulsoup 4。

要开始抓取网站，你需要 _requests_、_beautifulSoup4_ 和一个 _website_。

```sh
pip install requests
pip install beautifulsoup4
```

要从网站抓取数据，需要对 HTML 标签和 CSS 选择器有基本的了解。我们使用 HTML 标签、类（class）或/和 id 来定位网站上的内容。
让我们导入 requests 和 BeautifulSoup 模块

```py
import requests
from bs4 import BeautifulSoup
```

让我们声明一个 url 变量，用于指定我们要抓取的网站。

```py

import requests
from bs4 import BeautifulSoup
url = 'https://archive.ics.uci.edu/ml/datasets.php'

# 让我们使用 requests 的 get 方法从 url 获取数据

response = requests.get(url)
# 让我们检查状态
status = response.status_code
print(status) # 200 表示获取成功
```

```sh
200
```

使用 beautifulSoup 解析页面内容

```py
import requests
from bs4 import BeautifulSoup
url = 'https://archive.ics.uci.edu/ml/datasets.php'

response = requests.get(url)
content = response.content # 我们从网站获取所有内容
soup = BeautifulSoup(content, 'html.parser') # beautiful soup 将提供解析的机会
print(soup.title) # <title>UCI Machine Learning Repository: Data Sets</title>
print(soup.title.get_text()) # UCI Machine Learning Repository: Data Sets
print(soup.body) # 给出网站上的整个页面
print(response.status_code)

tables = soup.find_all('table', {'cellpadding':'3'})
# 我们定位 cellpadding 属性值为 3 的表格
# 我们可以使用 id、class 或 HTML 标签进行选择，更多信息请查看 beautifulsoup 文档
table = tables[0] # 结果是一个列表，我们从中提取数据
for td in table.find('tr').find_all('td'):
    print(td.text)
```

如果你运行这段代码，你会发现提取工作完成了一半。你可以继续完成它，因为这是练习 1 的一部分。
供参考，请查看 [beautifulsoup 文档](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#quick-start)

🌕 你非常特别，每天都在进步。距离你走向伟大只剩下八天了。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 22 天

1. 抓取以下网站并将数据存储为 json 文件（url = 'http://www.bu.edu/president/boston-university-facts-stats/'）。
2. 从这个 url（https://archive.ics.uci.edu/ml/datasets.php）中提取表格，并将其转换为 json 文件
3. 抓取总统表格并将数据存储为 json（https://en.wikipedia.org/wiki/List_of_presidents_of_the_United_States）。表格结构不太好，抓取可能会花费很长时间。

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 21 天](../21_Day_Classes_and_objects/21_classes_and_objects_类与对象.md) | [第 23 天 >>](../23_Day_Virtual_environment/23_virtual_environment_虚拟环境.md)
