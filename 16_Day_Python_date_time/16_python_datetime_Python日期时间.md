<div align="center">
  <h1> 🐍 30 Days Of Python：第 16 天 - Python 日期时间（Python Date time）</h1>
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

[<< 第 15 天](../15_Day_Python_type_errors/15_python_type_errors_Python类型错误.md) | [第 17 天 >>](../17_Day_Exception_handling/17_exception_handling_异常处理.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)
- [📘 第 16 天](#-第-16-天)
  - [Python *datetime*](#python-datetime)
    - [获取 *datetime* 信息](#获取-datetime-信息)
    - [使用 *strftime* 格式化日期输出](#使用-strftime-格式化日期输出)
    - [使用 *strptime* 将字符串转换为时间](#使用-strptime-将字符串转换为时间)
    - [使用 *datetime* 中的 *date*](#使用-datetime-中的-date)
    - [用时间对象表示时间](#用时间对象表示时间)
    - [计算两个时间点之间的差值](#计算两个时间点之间的差值)
    - [使用 *timedelta* 计算两个时间点之间的差值](#使用-timedelta-计算两个时间点之间的差值)
  - [💻 练习 - 第 16 天](#-练习---第-16-天)
# 📘 第 16 天

## Python *datetime*

Python 拥有 _datetime_ 模块来处理日期和时间。

```py
import datetime
print(dir(datetime))
['MAXYEAR', 'MINYEAR', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'date', 'datetime', 'datetime_CAPI', 'sys', 'time', 'timedelta', 'timezone', 'tzinfo']
```

通过 dir 或 help 内置命令（built-in command），可以了解某个模块中可用的函数。正如你所见，datetime 模块中有许多函数，但我们将重点关注 _date_、_datetime_、_time_ 和 _timedelta_。让我们逐一了解它们。

### 获取 *datetime* 信息

```py
from datetime import datetime
now = datetime.now()
print(now)                      # 2021-07-08 07:34:46.549883
day = now.day                   # 8
month = now.month               # 7
year = now.year                 # 2021
hour = now.hour                 # 7
minute = now.minute             # 38
second = now.second
timestamp = now.timestamp()
print(day, month, year, hour, minute)
print('timestamp', timestamp)
print(f'{day}/{month}/{year}, {hour}:{minute}')  # 8/7/2021, 7:38
```

时间戳（Timestamp）或 Unix 时间戳是指自 1970 年 1 月 1 日 UTC 起经过的秒数。

### 使用 *strftime* 格式化日期输出

```py
from datetime import datetime
new_year = datetime(2020, 1, 1)
print(new_year)      # 2020-01-01 00:00:00
day = new_year.day
month = new_year.month
year = new_year.year
hour = new_year.hour
minute = new_year.minute
second = new_year.second
print(day, month, year, hour, minute) #1 1 2020 0 0
print(f'{day}/{month}/{year}, {hour}:{minute}')  # 1/1/2020, 0:0

```

使用 *strftime* 方法格式化日期时间，相关文档可参考[这里](https://strftime.org/)。

```py
from datetime import datetime
# 当前日期和时间
now = datetime.now()
t = now.strftime("%H:%M:%S")
print("time:", t)           # time: 18:21:40
time_one = now.strftime("%m/%d/%Y, %H:%M:%S")
# mm/dd/YY H:M:S 格式
print("time one:", time_one)        # time one: 06/28/2022, 18:21:40
time_two = now.strftime("%d/%m/%Y, %H:%M:%S")
# dd/mm/YY H:M:S 格式
print("time two:", time_two)        # time two: 28/06/2022, 18:21:40
```

```sh
time: 01:05:01
time one: 12/05/2019, 01:05:01
time two: 05/12/2019, 01:05:01
```

以下是用于格式化时间的所有 _strftime_ 符号。本模块所有格式的示例。

![strftime](../images/strftime.png)

### 使用 *strptime* 将字符串转换为时间

这是一个帮助理解格式的[文档](https://www.programiz.com/python-programming/datetime/strptime)。

```py
from datetime import datetime
date_string = "5 December, 2019"
print("date_string =", date_string)     # date_string = 5 December, 2019
date_object = datetime.strptime(date_string, "%d %B, %Y")
print("date_object =", date_object)     # date_object = 2019-12-05 00:00:00
```

```sh
date_string = 5 December, 2019
date_object = 2019-12-05 00:00:00
```

### 使用 *datetime* 中的 *date*

```py
from datetime import date
d = date(2020, 1, 1)
print(d)        # 2020-01-01
print('Current date:', d.today())    # 2019-12-05
# 今日日期的 date 对象
today = date.today()
print("Current year:", today.year)   # 2019
print("Current month:", today.month) # 12
print("Current day:", today.day)     # 5
```

### 用时间对象表示时间

```py
from datetime import time
# time(hour = 0, minute = 0, second = 0)
a = time()
print("a =", a)     # a = 00:00:00
# time(hour, minute and second)
b = time(10, 30, 50)
print("b =", b)     # b = 10:30:50
# time(hour, minute and second)
c = time(hour=10, minute=30, second=50)
print("c =", c)     # c = 10:30:50
# time(hour, minute, second, microsecond)
d = time(10, 30, 50, 200555)
print("d =", d)     # d = 10:30:50.200555
```

输出（output）  
a = 00:00:00  
b = 10:30:50  
c = 10:30:50  
d = 10:30:50.200555

### 计算两个时间点之间的差值

```py
from datetime import date, datetime
today = date(year=2019, month=12, day=5)
new_year = date(year=2020, month=1, day=1)
time_left_for_newyear = new_year - today
# 距离新年还有：27 天, 0:00:00
print('Time left for new year: ', time_left_for_newyear)  # Time left for new year:  27 days, 0:00:00

t1 = datetime(year = 2019, month = 12, day = 5, hour = 0, minute = 59, second = 0)
t2 = datetime(year = 2020, month = 1, day = 1, hour = 0, minute = 0, second = 0)
diff = t2 - t1
print('Time left for new year:', diff) # Time left for new year: 26 days, 23: 01: 00
```

### 使用 *timedelta* 计算两个时间点之间的差值

```py
from datetime import timedelta
t1 = timedelta(weeks=12, days=10, hours=4, seconds=20)
t2 = timedelta(days=7, hours=5, minutes=3, seconds=30)
t3 = t1 - t2
print("t3 =", t3)
```

```sh
    date_string = 5 December, 2019
    date_object = 2019-12-05 00:00:00
    t3 = 86 days, 22:56:50
```

🌕 你是一个非凡的人。在通往伟大的道路上，你已经领先了 16 步。现在为你的大脑和肌肉做一些练习吧。

## 💻 练习 - 第 16 天

1. 从 datetime 模块获取当前的天、月、年、小时、分钟和时间戳（timestamp）。
2. 使用以下格式格式化当前日期："%m/%d/%Y, %H:%M:%S"
3. 今天是 2019 年 12 月 5 日。将这个时间字符串转换为时间对象。
4. 计算当前时间与新年之间的时间差。
5. 计算 1970 年 1 月 1 日与现在之间的时间差。
6. 思考一下，datetime 模块可以用来做什么？示例：
   - 时间序列分析（Time series analysis）
   - 获取应用中任何活动的时间戳
   - 在博客上添加文章

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 15 天](../15_Day_Python_type_errors/15_python_type_errors_Python类型错误.md) | [第 17 天 >>](../17_Day_Exception_handling/17_exception_handling_异常处理.md)
