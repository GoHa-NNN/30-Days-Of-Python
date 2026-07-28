<div align="center">
  <h1> 🐍 30 Days Of Python：第 25 天 - Pandas</h1>
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

[<< 第 24 天](../24_Day_Statistics/24_statistics_统计学.md) | [第 26 天 >>](../26_Day_Python_web/26_python_web_Python_Web开发.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 25 天](#-第-25-天)
  - [Pandas](#pandas)
    - [安装 Pandas](#安装-pandas)
    - [导入 Pandas](#导入-pandas)
    - [创建带有默认索引的 Pandas Series](#创建带有默认索引的-pandas-series)
    - [创建带有自定义索引的 Pandas Series](#创建带有自定义索引的-pandas-series)
    - [从字典创建 Pandas Series](#从字典创建-pandas-series)
    - [创建常量 Pandas Series](#创建常量-pandas-series)
    - [使用 Linspace 创建 Pandas Series](#使用-linspace-创建-pandas-series)
  - [DataFrame](#dataframe)
    - [从列表的列表创建 DataFrame](#从列表的列表创建-dataframe)
    - [使用字典创建 DataFrame](#使用字典创建-dataframe)
    - [从字典列表创建 DataFrame](#从字典列表创建-dataframe)
  - [使用 Pandas 读取 CSV 文件](#使用-pandas-读取-csv-文件)
    - [数据探索](#数据探索)
  - [修改 DataFrame](#修改-dataframe)
    - [创建 DataFrame](#创建-dataframe)
    - [添加新列](#添加新列)
    - [修改列值](#修改列值)
    - [格式化 DataFrame 列](#格式化-dataframe-列)
  - [检查列值的数据类型](#检查列值的数据类型)
    - [布尔索引](#布尔索引)
  - [💻 练习 - 第 25 天](#-练习---第-25-天)

# 📘 第 25 天

## Pandas

Pandas 是一个开源的、高性能的、易用的 Python 编程语言数据结构和数据分析工具。
Pandas 添加了旨在处理表格数据的数据结构和工具，即 *Series* 和 *Data Frames*。
Pandas 提供了数据操作工具：

- 重塑（reshaping）
- 合并（merging）
- 排序（sorting）
- 切片（slicing）
- 聚合（aggregation）
- 插补（imputation）。
如果你使用的是 anaconda，则不需要安装 pandas。

### 安装 Pandas

对于 Mac：
```py
pip install conda
conda install pandas
```

对于 Windows：
```py
pip install conda
pip install pandas
```

Pandas 数据结构基于 *Series* 和 *DataFrame*。

*series* 是一个 *列（column）*，而 DataFrame 是由 *series* 集合组成的 *多维表格（multidimensional table）*。为了创建 pandas series，我们应该使用 numpy 创建一维数组或 python 列表。
让我们看一个 series 的示例：

名称 Pandas Series

![pandas series](../images/pandas-series-1.png)

国家 Series

![pandas series](../images/pandas-series-2.png)

城市 Series

![pandas series](../images/pandas-series-3.png)

如你所见，pandas series 只是一列数据。如果我们想要多列，我们就使用数据框（data frame）。下面的示例展示了 pandas DataFrame。

让我们看一个 pandas 数据框的示例：

![Pandas data frame](../images/pandas-dataframe-1.png)

数据框是行和 columns 的集合。看下面的表格；它比上面的示例有更多的列：

![Pandas data frame](../images/pandas-dataframe-2.png)

接下来，我们将了解如何导入 pandas 以及如何使用 pandas 创建 Series 和 DataFrame

### 导入 Pandas

```python
import pandas as pd # 将 pandas 导入为 pd
import numpy  as np # 将 numpy 导入为 np
```

### 创建带有默认索引的 Pandas Series

```python
nums = [1, 2, 3, 4,5]
s = pd.Series(nums)
print(s)
```

```sh
    0    1
    1    2
    2    3
    3    4
    4    5
    dtype: int64
```

### 创建带有自定义索引的 Pandas Series

```python
nums = [1, 2, 3, 4, 5]
s = pd.Series(nums, index=[1, 2, 3, 4, 5])
print(s)
```

```sh
    1    1
    2    2
    3    3
    4    4
    5    5
    dtype: int64
```

```python
fruits = ['Orange','Banana','Mango']
fruits = pd.Series(fruits, index=[1, 2, 3])
print(fruits)
```

```sh
    1    Orange
    2    Banana
    3    Mango
    dtype: object
```

### 从字典创建 Pandas Series

```python
dct = {'name':'Asabeneh','country':'Finland','city':'Helsinki'}
```

```python
s = pd.Series(dct)
print(s)
```

```sh
    name       Asabeneh
    country     Finland
    city       Helsinki
    dtype: object
```

### 创建常量 Pandas Series

```python
s = pd.Series(10, index = [1, 2, 3])
print(s)
```

```sh
    1    10
    2    10
    3    10
    dtype: int64
```

### 使用 Linspace 创建 Pandas Series

```python
s = pd.Series(np.linspace(5, 20, 10)) # linspace(starting, end, items)
print(s)
```

```sh
    0     5.000000
    1     6.666667
    2     8.333333
    3    10.000000
    4    11.666667
    5    13.333333
    6    15.000000
    7    16.666667
    8    18.333333
    9    20.000000
    dtype: float64
```

## DataFrame

Pandas 数据框可以通过不同的方式创建。

### 从列表的列表创建 DataFrame

```python
data = [
    ['Asabeneh', 'Finland', 'Helsink'],
    ['David', 'UK', 'London'],
    ['John', 'Sweden', 'Stockholm']
]
df = pd.DataFrame(data, columns=['Names','Country','City'])
print(df)
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Names</th>
      <th>Country</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Asabeneh</td>
      <td>Finland</td>
      <td>Helsink</td>
    </tr>
    <tr>
      <td>1</td>
      <td>David</td>
      <td>UK</td>
      <td>London</td>
    </tr>
    <tr>
      <td>2</td>
      <td>John</td>
      <td>Sweden</td>
      <td>Stockholm</td>
    </tr>
  </tbody>
</table>

### 使用字典创建 DataFrame

```python
data = {'Name': ['Asabeneh', 'David', 'John'], 'Country':[
    'Finland', 'UK', 'Sweden'], 'City': ['Helsiki', 'London', 'Stockholm']}
df = pd.DataFrame(data)
print(df)
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Country</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Asabeneh</td>
      <td>Finland</td>
      <td>Helsiki</td>
    </tr>
    <tr>
      <td>1</td>
      <td>David</td>
      <td>UK</td>
      <td>London</td>
    </tr>
    <tr>
      <td>2</td>
      <td>John</td>
      <td>Sweden</td>
      <td>Stockholm</td>
    </tr>
  </tbody>
</table>

### 从字典列表创建 DataFrame

```python
data = [
    {'Name': 'Asabeneh', 'Country': 'Finland', 'City': 'Helsinki'},
    {'Name': 'David', 'Country': 'UK', 'City': 'London'},
    {'Name': 'John', 'Country': 'Sweden', 'City': 'Stockholm'}]
df = pd.DataFrame(data)
print(df)
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Country</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Asabeneh</td>
      <td>Finland</td>
      <td>Helsinki</td>
    </tr>
    <tr>
      <td>1</td>
      <td>David</td>
      <td>UK</td>
      <td>London</td>
    </tr>
    <tr>
      <td>2</td>
      <td>John</td>
      <td>Sweden</td>
      <td>Stockholm</td>
    </tr>
  </tbody>
</table>

## 使用 Pandas 读取 CSV 文件

要下载本示例所需的 CSV 文件，控制台/命令行就足够了：

```sh
curl -O https://raw.githubusercontent.com/Asabeneh/30-Days-Of-Python/master/data/weight-height.csv
```

将下载的文件放在你的工作目录中。

```python
import pandas as pd

df = pd.read_csv('weight-height.csv')
print(df)
```

### 数据探索

让我们使用 head() 只读取前 5 行

```python
print(df.head()) # 给出五行，我们可以通过向 head() 方法传递参数来增加行数
```


<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Height</th>
      <th>Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Male</td>
      <td>73.847017</td>
      <td>241.893563</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Male</td>
      <td>68.781904</td>
      <td>162.310473</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Male</td>
      <td>74.110105</td>
      <td>212.740856</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Male</td>
      <td>71.730978</td>
      <td>220.042470</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Male</td>
      <td>69.881796</td>
      <td>206.349801</td>
    </tr>
  </tbody>
</table>

让我们还使用 tail() 方法探索数据框的最后记录。

```python
print(df.tail()) # tail 给出最后五行，我们可以通过向 tail 方法传递参数来增加行数
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Height</th>
      <th>Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>9995</td>
      <td>Female</td>
      <td>66.172652</td>
      <td>136.777454</td>
    </tr>
    <tr>
      <td>9996</td>
      <td>Female</td>
      <td>67.067155</td>
      <td>170.867906</td>
    </tr>
    <tr>
      <td>9997</td>
      <td>Female</td>
      <td>63.867992</td>
      <td>128.475319</td>
    </tr>
    <tr>
      <td>9998</td>
      <td>Female</td>
      <td>69.034243</td>
      <td>163.852461</td>
    </tr>
    <tr>
      <td>9999</td>
      <td>Female</td>
      <td>61.944246</td>
      <td>113.649103</td>
    </tr>
  </tbody>
</table>

如你所见，csv 文件有三行：Gender、Height 和 Weight。如果 DataFrame 有很多行，将很难知道所有的列。因此，我们应该使用一个方法来了解列。我们不知道行数。让我们使用 shape 方法。

```python
print(df.shape) # 如你所见，10000 行和三列
```

    (10000, 3)

让我们使用 columns 获取所有列。

```python
print(df.columns)
```

    Index(['Gender', 'Height', 'Weight'], dtype='object')

现在，让我们使用列键获取特定列

```python
heights = df['Height'] # 这现在是一个 series
```

```python
print(heights)
```

```sh
    0       73.847017
    1       68.781904
    2       74.110105
    3       71.730978
    4       69.881796
              ...
    9995    66.172652
    9996    67.067155
    9997    63.867992
    9998    69.034243
    9999    61.944246
    Name: Height, Length: 10000, dtype: float64
```

```python
weights = df['Weight'] # 这现在是一个 series
```

```python
print(weights)
```

```sh
    0       241.893563
    1       162.310473
    2       212.740856
    3       220.042470
    4       206.349801
               ...
    9995    136.777454
    9996    170.867906
    9997    128.475319
    9998    163.852461
    9999    113.649103
    Name: Weight, Length: 10000, dtype: float64
```

```python
print(len(heights) == len(weights))
```

    True

describe() 方法提供数据集的描述性统计值。

```python
print(heights.describe()) # 给出关于身高数据的统计信息
```

```sh
    count    10000.000000
    mean        66.367560
    std          3.847528
    min         54.263133
    25%         63.505620
    50%         66.318070
    75%         69.174262
    max         78.998742
    Name: Height, dtype: float64
```

```python
print(weights.describe())
```

```sh
    count    10000.000000
    mean       161.440357
    std         32.108439
    min         64.700127
    25%        135.818051
    50%        161.212928
    75%        187.169525
    max        269.989699
    Name: Weight, dtype: float64
```

```python
print(df.describe())  # describe 也可以从 DataFrame 给出统计信息
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Height</th>
      <th>Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>count</td>
      <td>10000.000000</td>
      <td>10000.000000</td>
    </tr>
    <tr>
      <td>mean</td>
      <td>66.367560</td>
      <td>161.440357</td>
    </tr>
    <tr>
      <td>std</td>
      <td>3.847528</td>
      <td>32.108439</td>
    </tr>
    <tr>
      <td>min</td>
      <td>54.263133</td>
      <td>64.700127</td>
    </tr>
    <tr>
      <td>25%</td>
      <td>63.505620</td>
      <td>135.818051</td>
    </tr>
    <tr>
      <td>50%</td>
      <td>66.318070</td>
      <td>161.212928</td>
    </tr>
    <tr>
      <td>75%</td>
      <td>69.174262</td>
      <td>187.169525</td>
    </tr>
    <tr>
      <td>max</td>
      <td>78.998742</td>
      <td>269.989699</td>
    </tr>
  </tbody>
</table>

与 describe() 类似，info() 方法也提供关于数据集的信息。

## 修改 DataFrame

修改 DataFrame：
    * 我们可以创建一个新的 DataFrame
    * 我们可以创建一个新列并将其添加到 DataFrame 中，
    * 我们可以从 DataFrame 中移除现有列，
    * 我们可以修改 DataFrame 中的现有列，
    * 我们可以更改 DataFrame 中列值的数据类型

### 创建 DataFrame

一如既往，首先我们导入必要的包。现在，让我们导入 pandas 和 numpy，两个最好的朋友。

```python
import pandas as pd
import numpy as np
data = [
    {"Name": "Asabeneh", "Country":"Finland","City":"Helsinki"},
    {"Name": "David", "Country":"UK","City":"London"},
    {"Name": "John", "Country":"Sweden","City":"Stockholm"}]
df = pd.DataFrame(data)
print(df)
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Country</th>
      <th>City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Asabeneh</td>
      <td>Finland</td>
      <td>Helsinki</td>
    </tr>
    <tr>
      <td>1</td>
      <td>David</td>
      <td>UK</td>
      <td>London</td>
    </tr>
    <tr>
      <td>2</td>
      <td>John</td>
      <td>Sweden</td>
      <td>Stockholm</td>
    </tr>
  </tbody>
</table>

向 DataFrame 添加列就像向字典添加键一样。

首先让我们使用前面的示例创建 DataFrame。创建 DataFrame 后，我们将开始修改列和列值。

### 添加新列

让我们在 DataFrame 中添加一个 weight 列

```python
weights = [74, 78, 69]
df['Weight'] = weights
df
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Country</th>
      <th>City</th>
      <th>Weight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Asabeneh</td>
      <td>Finland</td>
      <td>Helsinki</td>
      <td>74</td>
    </tr>
    <tr>
      <td>1</td>
      <td>David</td>
      <td>UK</td>
      <td>London</td>
      <td>78</td>
    </tr>
    <tr>
      <td>2</td>
      <td>John</td>
      <td>Sweden</td>
      <td>Stockholm</td>
      <td>69</td>
    </tr>
  </tbody>
</table>

让我们也在 DataFrame 中添加一个 height 列

```python
heights = [173, 175, 169]
df['Height'] = heights
print(df)
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Country</th>
      <th>City</th>
      <th>Weight</th>
      <th>Height</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Asabeneh</td>
      <td>Finland</td>
      <td>Helsinki</td>
      <td>74</td>
      <td>173</td>
    </tr>
    <tr>
      <td>1</td>
      <td>David</td>
      <td>UK</td>
      <td>London</td>
      <td>78</td>
      <td>175</td>
    </tr>
    <tr>
      <td>2</td>
      <td>John</td>
      <td>Sweden</td>
      <td>Stockholm</td>
      <td>69</td>
      <td>169</td>
    </tr>
  </tbody>
</table>

如你在上面的 DataFrame 中所见，我们确实添加了新的列 Weight 和 Height。让我们通过计算他们的 BMI（身体质量指数）来添加一个名为 BMI 的额外列。BMI 是质量除以身高（以米为单位）的平方 - Weight/Height * Height。

如你所见，身高是厘米，所以我们应该将其改为米。让我们修改身高行。

### 修改列值

```python
df['Height'] = df['Height'] * 0.01
df
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Country</th>
      <th>City</th>
      <th>Weight</th>
      <th>Height</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Asabeneh</td>
      <td>Finland</td>
      <td>Helsinki</td>
      <td>74</td>
      <td>1.73</td>
    </tr>
    <tr>
      <td>1</td>
      <td>David</td>
      <td>UK</td>
      <td>London</td>
      <td>78</td>
      <td>1.75</td>
    </tr>
    <tr>
      <td>2</td>
      <td>John</td>
      <td>Sweden</td>
      <td>Stockholm</td>
      <td>69</td>
      <td>1.69</td>
    </tr>
  </tbody>
</table>

```python
# 使用函数让我们的代码更简洁，但你也可以不用函数计算 bmi
def calculate_bmi ():
    weights = df['Weight']
    heights = df['Height']
    bmi = []
    for w,h in zip(weights, heights):
        b = w/(h*h)
        bmi.append(b)
    return bmi

bmi = calculate_bmi()

```


```python
df['BMI'] = bmi
df
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Country</th>
      <th>City</th>
      <th>Weight</th>
      <th>Height</th>
      <th>BMI</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Asabeneh</td>
      <td>Finland</td>
      <td>Helsinki</td>
      <td>74</td>
      <td>1.73</td>
      <td>24.725183</td>
    </tr>
    <tr>
      <td>1</td>
      <td>David</td>
      <td>UK</td>
      <td>London</td>
      <td>78</td>
      <td>1.75</td>
      <td>25.469388</td>
    </tr>
    <tr>
      <td>2</td>
      <td>John</td>
      <td>Sweden</td>
      <td>Stockholm</td>
      <td>69</td>
      <td>1.69</td>
      <td>24.158818</td>
    </tr>
  </tbody>
</table>

### 格式化 DataFrame 列

DataFrame 的 BMI 列值是浮点数，小数点后有许多有效数字。让我们将其改为小数点后一位有效数字。

```python
df['BMI'] = round(df['BMI'], 1)
print(df)
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Country</th>
      <th>City</th>
      <th>Weight</th>
      <th>Height</th>
      <th>BMI</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Asabeneh</td>
      <td>Finland</td>
      <td>Helsinki</td>
      <td>74</td>
      <td>1.73</td>
      <td>24.7</td>
    </tr>
    <tr>
      <td>1</td>
      <td>David</td>
      <td>UK</td>
      <td>London</td>
      <td>78</td>
      <td>1.75</td>
      <td>25.5</td>
    </tr>
    <tr>
      <td>2</td>
      <td>John</td>
      <td>Sweden</td>
      <td>Stockholm</td>
      <td>69</td>
      <td>1.69</td>
      <td>24.2</td>
    </tr>
  </tbody>
</table>

DataFrame 中的信息似乎还不完整，让我们添加出生年份和当前年份列。

```python
birth_year = ['1769', '1985', '1990']
current_year = pd.Series(2020, index=[0, 1,2])
df['Birth Year'] = birth_year
df['Current Year'] = current_year
df
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Country</th>
      <th>City</th>
      <th>Weight</th>
      <th>Height</th>
      <th>BMI</th>
      <th>Birth Year</th>
      <th>Current Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Asabeneh</td>
      <td>Finland</td>
      <td>Helsinki</td>
      <td>74</td>
      <td>1.73</td>
      <td>24.7</td>
      <td>1769</td>
      <td>2020</td>
    </tr>
    <tr>
      <td>1</td>
      <td>David</td>
      <td>UK</td>
      <td>London</td>
      <td>78</td>
      <td>1.75</td>
      <td>25.5</td>
      <td>1985</td>
      <td>2020</td>
    </tr>
    <tr>
      <td>2</td>
      <td>John</td>
      <td>Sweden</td>
      <td>Stockholm</td>
      <td>69</td>
      <td>1.69</td>
      <td>24.2</td>
      <td>1990</td>
      <td>2020</td>
    </tr>
  </tbody>
</table>

## 检查列值的数据类型

```python
print(df.Weight.dtype)
```

```sh
    dtype('int64')
```

```python
df['Birth Year'].dtype # 它给出字符串对象，我们应该将其更改为数字

```

```python
df['Birth Year'] = df['Birth Year'].astype('int')
print(df['Birth Year'].dtype) # 让我们现在检查数据类型
```

```sh
    dtype('int32')
```

现在对当前年份做同样的操作：

```python
df['Current Year'] = df['Current Year'].astype('int')
df['Current Year'].dtype
```

```sh
    dtype('int32')
```

现在，出生年份和当前年份的列值是整数。我们可以计算年龄。

```python
ages = df['Current Year'] - df['Birth Year']
ages
```

    0    251
    1     35
    2     30
    dtype: int32

```python
df['Ages'] = ages
print(df)
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Country</th>
      <th>City</th>
      <th>Weight</th>
      <th>Height</th>
      <th>BMI</th>
      <th>Birth Year</th>
      <th>Current Year</th>
      <th>Ages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Asabeneh</td>
      <td>Finland</td>
      <td>Helsinki</td>
      <td>74</td>
      <td>1.73</td>
      <td>24.7</td>
      <td>1769</td>
      <td>2019</td>
      <td>250</td>
    </tr>
    <tr>
      <td>1</td>
      <td>David</td>
      <td>UK</td>
      <td>London</td>
      <td>78</td>
      <td>1.75</td>
      <td>25.5</td>
      <td>1985</td>
      <td>2019</td>
      <td>34</td>
    </tr>
    <tr>
      <td>2</td>
      <td>John</td>
      <td>Sweden</td>
      <td>Stockholm</td>
      <td>69</td>
      <td>1.69</td>
      <td>24.2</td>
      <td>1990</td>
      <td>2019</td>
      <td>29</td>
    </tr>
  </tbody>
</table>

第一行中的人到目前为止活了 251 年。对某人来说活这么长时间是不太可能的。要么是拼写错误，要么是数据被篡改了。所以让我们用不包含异常值的列平均值来填充该数据。

mean = (35 + 30)/ 2

```python
mean = (35 + 30)/ 2
print('Mean: ',mean)	# 在输出中添加一些描述是好的，这样我们就知道是什么了
```

```sh
   Mean:  32.5
```

### 布尔索引

```python
print(df[df['Ages'] > 120])
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Country</th>
      <th>City</th>
      <th>Weight</th>
      <th>Height</th>
      <th>BMI</th>
      <th>Birth Year</th>
      <th>Current Year</th>
      <th>Ages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Asabeneh</td>
      <td>Finland</td>
      <td>Helsinki</td>
      <td>74</td>
      <td>1.73</td>
      <td>24.7</td>
      <td>1769</td>
      <td>2020</td>
      <td>251</td>
    </tr>
  </tbody>
</table>


```python
print(df[df['Ages'] < 120])
```

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Country</th>
      <th>City</th>
      <th>Weight</th>
      <th>Height</th>
      <th>BMI</th>
      <th>Birth Year</th>
      <th>Current Year</th>
      <th>Ages</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>David</td>
      <td>UK</td>
      <td>London</td>
      <td>78</td>
      <td>1.75</td>
      <td>25.5</td>
      <td>1985</td>
      <td>2020</td>
      <td>35</td>
    </tr>
    <tr>
      <td>2</td>
      <td>John</td>
      <td>Sweden</td>
      <td>Stockholm</td>
      <td>69</td>
      <td>1.69</td>
      <td>24.2</td>
      <td>1990</td>
      <td>2020</td>
      <td>30</td>
    </tr>
  </tbody>
</table>

## 💻 练习 - 第 25 天

1. 从数据目录读取 hacker_news.csv 文件
1. 获取前五行
1. 获取最后五行
1. 将 title 列作为 pandas series 获取
1. 计算行数和列数
    - 过滤包含 python 的标题
    - 过滤包含 JavaScript 的标题
    - 探索数据并理解它

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 24 天](../24_Day_Statistics/24_statistics_统计学.md) | [第 26 天 >>](../26_Day_Python_web/26_python_web_Python_Web开发.md)
