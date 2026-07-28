<div align="center">
  <h1> 🐍 30 Days Of Python：第 27 天 - Python 与 MongoDB</h1>
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

[<< 第 26 天](../26_Day_Python_web/26_python_web_Python_Web开发.md) | [第 28 天 >>](../28_Day_API/28_API_API.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 27 天](#-第-27-天)
- [Python 与 MongoDB](#python-与-mongodb)
  - [MongoDB](#mongodb)
    - [SQL 与 NoSQL 的对比](#sql-与-nosql-的对比)
    - [获取连接字符串（MongoDB URI）](#获取连接字符串mongodb-uri)
    - [将 Flask 应用程序连接到 MongoDB 集群](#将-flask-应用程序连接到-mongodb-集群)
    - [创建数据库和集合](#创建数据库和集合)
    - [向集合插入多个文档](#向集合插入多个文档)
    - [MongoDB 查找（Find）](#mongodb-查找find)
    - [带查询条件的查找](#带查询条件的查找)
    - [带修饰符的查询](#带修饰符的查询)
    - [限制文档数量](#限制文档数量)
    - [带排序的查找](#带排序的查找)
    - [带查询条件的更新](#带查询条件的更新)
    - [删除文档](#删除文档)
    - [删除集合](#删除集合)
  - [💻 练习 - 第 27 天](#-练习---第-27-天)

# 📘 第 27 天

# Python 与 MongoDB

Python 是一种后端（backend）技术，它可以与不同的数据库应用程序连接。它可以连接 SQL 和 NoSQL 数据库。在本节中，我们将 Python 与 MongoDB 数据库（一种 NoSQL 数据库）连接起来。

## MongoDB

MongoDB 是一种 NoSQL 数据库。MongoDB 以类似 JSON 的文档（document）形式存储数据，这使得 MongoDB 非常灵活且可扩展。让我们看看 SQL 和 NoSQL 数据库的不同术语。下表将展示 SQL 与 NoSQL 数据库之间的区别。

### SQL 与 NoSQL 的对比

![SQL 与 NoSQL 对比](../images/mongoDB/sql-vs-nosql.png)

在本节中，我们将重点介绍 NoSQL 数据库 MongoDB。让我们在 [mongoDB](https://www.mongodb.com/) 上注册账号，点击登录按钮，然后在下一页点击注册。

![MongoDB 注册页面](../images/mongoDB/mongodb-signup-page.png)

填写字段并点击继续

![MongoDB 注册](../images/mongoDB/mongodb-register.png)

选择免费套餐（free plan）

![MongoDB 免费套餐](../images/mongoDB/mongodb-free.png)

选择就近的免费区域，并为你的集群（cluster）起一个名字。

![MongoDB 集群名称](../images/mongoDB/mongodb-cluster-name.png)

现在，一个免费的沙盒（sandbox）已创建

![MongoDB 沙盒](../images/mongoDB/mongodb-sandbox.png)

允许所有本地主机访问

![MongoDB 允许 IP 访问](../images/mongoDB/mongodb-allow-ip-access.png)

添加用户和密码

![MongoDB 添加用户](../images/mongoDB/mongodb-add-user.png)

创建 MongoDB URI 链接

![MongoDB 创建 URI](../images/mongoDB/mongodb-create-uri.png)

选择 Python 3.6 或更高版本的驱动程序（driver）

![MongoDB Python 驱动程序](../images/mongoDB/mongodb-python-driver.png)

### 获取连接字符串（MongoDB URI）

复制连接字符串链接，你将得到类似以下的内容：

```sh
mongodb+srv://asabeneh:<password>@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority
```

不要担心这个 URL，它是将你的应用程序与 mongoDB 连接的一种方式。
让我们将密码占位符替换为你添加用户时使用的密码。

**示例：**

```sh
mongodb+srv://asabeneh:123123123@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority
```

现在，我已经替换了所有内容，密码是 123123，数据库名称是 *thirty_days_python*。这只是一个示例，你的密码必须比示例密码更强。

Python 需要一个 mongoDB 驱动程序来访问 mongoDB 数据库。我们将使用 _pymongo_ 配合 _dnspython_ 来连接我们的应用程序与 mongoDB。在你的项目目录中安装 pymongo 和 dnspython。

```sh
pip install pymongo dnspython
```

要使用 mongodb+srv:// URI，必须安装 "dnspython" 模块。dnspython 是 Python 的 DNS 工具包。它支持几乎所有记录类型。

### 将 Flask 应用程序连接到 MongoDB 集群

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
print(client.list_database_names())

app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)

```

当我们运行上面的代码时，会得到默认的 mongoDB 数据库。

```sh
['admin', 'local']
```

### 创建数据库和集合

让我们创建一个数据库，如果数据库和集合在 mongoDB 中不存在，它们将被创建。让我们创建一个名为 *thirty_days_of_python* 的数据库和一个 *students* 集合。

创建数据库：

```sh
db = client.name_of_databse # 我们可以这样创建数据库，或者用第二种方式
db = client['name_of_database']
```

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
# 创建数据库
db = client.thirty_days_of_python
# 创建 students 集合并插入一个文档
db.students.insert_one({'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'age': 250})
print(client.list_database_names())

app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

创建数据库后，我们还创建了一个 students 集合并使用 *insert_one()* 方法插入了一个文档。
现在，数据库 *thirty_days_of_python* 和 *students* 集合已创建，文档也已插入。
检查你的 mongoDB 集群，你将看到数据库和集合。集合内部会有一个文档。

```sh
['thirty_days_of_python', 'admin', 'local']
```

如果你在 mongoDB 集群上看到这个，说明你已经成功创建了一个数据库和一个集合。

![创建数据库和集合](../images/mongoDB/mongodb-creating_database.png)

如果你在图中看到，文档创建时带有一个长 ID，它充当主键（primary key）。每次我们创建一个文档，mongoDB 都会为其创建一个唯一的 ID。

### 向集合插入多个文档

*insert_one()* 方法一次插入一个条目，如果我们想一次插入多个文档，可以使用 *insert_many()* 方法或 for 循环。
我们可以使用 for 循环一次插入多个文档。

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)

students = [
        {'name':'David','country':'UK','city':'London','age':34},
        {'name':'John','country':'Sweden','city':'Stockholm','age':28},
        {'name':'Sami','country':'Finland','city':'Helsinki','age':25},
    ]
for student in students:
    db.students.insert_one(student)


app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

### MongoDB 查找（Find）

*find()* 和 *findOne()* 方法是在 mongoDB 数据库的集合中查找数据的常用方法。它类似于 MySQL 数据库中的 SELECT 语句。
让我们使用 _find_one()_ 方法来获取数据库集合中的一个文档。

- \*find_one({"\_id": ObjectId("id")}): 如果未提供 id，则获取第一个匹配项

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库
student = db.students.find_one()
print(student)


app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)

```

```sh
{'_id': ObjectId('5df68a21f106fe2d315bbc8b'), 'name': 'Asabeneh', 'country': 'Helsinki', 'city': 'Helsinki', 'age': 250}
```

上面的查询返回第一个条目，但我们可以通过特定的 \_id 来定位特定文档。让我们做一个示例，使用 David 的 id 来获取 David 对象。
'\_id':ObjectId('5df68a23f106fe2d315bbc8c')

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
from bson.objectid import ObjectId # id 对象
MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库
student = db.students.find_one({'_id':ObjectId('5df68a23f106fe2d315bbc8c')})
print(student)

app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

```sh
{'_id': ObjectId('5df68a23f106fe2d315bbc8c'), 'name': 'David', 'country': 'UK', 'city': 'London', 'age': 34}
```

我们已经通过上面的示例了解了如何使用 _find_one()_。让我们继续学习 _find()_

- _find()_: 如果我们不传递查询对象，则返回集合中的所有匹配项。该对象是 pymongo.cursor 对象。

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块

MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库
students = db.students.find()
for student in students:
    print(student)

app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

```sh
{'_id': ObjectId('5df68a21f106fe2d315bbc8b'), 'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'age': 250}
{'_id': ObjectId('5df68a23f106fe2d315bbc8c'), 'name': 'David', 'country': 'UK', 'city': 'London', 'age': 34}
{'_id': ObjectId('5df68a23f106fe2d315bbc8d'), 'name': 'John', 'country': 'Sweden', 'city': 'Stockholm', 'age': 28}
{'_id': ObjectId('5df68a23f106fe2d315bbc8e'), 'name': 'Sami', 'country': 'Finland', 'city': 'Helsinki', 'age': 25}
```

我们可以通过在 _find({}, {})_ 中传递第二个对象来指定要返回的字段。0 表示不包含，1 表示包含，但我们不能混合使用 0 和 1，\_id 除外。

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块

MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库
students = db.students.find({}, {"_id":0,  "name": 1, "country":1}) # 0 表示不包含，1 表示包含
for student in students:
    print(student)

app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

```sh
{'name': 'Asabeneh', 'country': 'Finland'}
{'name': 'David', 'country': 'UK'}
{'name': 'John', 'country': 'Sweden'}
{'name': 'Sami', 'country': 'Finland'}
```

### 带查询条件的查找

在 mongoDB 中，find 接受一个查询对象。我们可以传递一个查询对象来过滤我们想要过滤的文档。

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块

MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库

query = {
    "country":"Finland"
}
students = db.students.find(query)

for student in students:
    print(student)


app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

```sh
{'_id': ObjectId('5df68a21f106fe2d315bbc8b'), 'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'age': 250}
{'_id': ObjectId('5df68a23f106fe2d315bbc8e'), 'name': 'Sami', 'country': 'Finland', 'city': 'Helsinki', 'age': 25}
```

带修饰符的查询

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
import pymongo

MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库

query = {
    "city":"Helsinki"
}
students = db.students.find(query)
for student in students:
    print(student)


app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

```sh
{'_id': ObjectId('5df68a21f106fe2d315bbc8b'), 'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'age': 250}
{'_id': ObjectId('5df68a23f106fe2d315bbc8e'), 'name': 'Sami', 'country': 'Finland', 'city': 'Helsinki', 'age': 25}
```

### 带修饰符的查询

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
import pymongo

MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库
query = {
    "country":"Finland",
    "city":"Helsinki"
}
students = db.students.find(query)
for student in students:
    print(student)


app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

```sh
{'_id': ObjectId('5df68a21f106fe2d315bbc8b'), 'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'age': 250}
{'_id': ObjectId('5df68a23f106fe2d315bbc8e'), 'name': 'Sami', 'country': 'Finland', 'city': 'Helsinki', 'age': 25}
```

带修饰符的查询

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
import pymongo

MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库
query = {"age":{"$gt":30}}
students = db.students.find(query)
for student in students:
    print(student)

app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

```sh
{'_id': ObjectId('5df68a21f106fe2d315bbc8b'), 'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'age': 250}
{'_id': ObjectId('5df68a23f106fe2d315bbc8c'), 'name': 'David', 'country': 'UK', 'city': 'London', 'age': 34}
```

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
import pymongo

MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库
query = {"age":{"$gt":30}}
students = db.students.find(query)
for student in students:
    print(student)
```

```sh
{'_id': ObjectId('5df68a23f106fe2d315bbc8d'), 'name': 'John', 'country': 'Sweden', 'city': 'Stockholm', 'age': 28}
{'_id': ObjectId('5df68a23f106fe2d315bbc8e'), 'name': 'Sami', 'country': 'Finland', 'city': 'Helsinki', 'age': 25}
```

### 限制文档数量

我们可以使用 _limit()_ 方法来限制返回的文档数量。

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
import pymongo

MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库
db.students.find().limit(3)
```

### 带排序的查找

默认情况下，排序为升序（ascending order）。我们可以通过添加 -1 参数将排序改为降序（descending order）。

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
import pymongo

MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库
students = db.students.find().sort('name')
for student in students:
    print(student)


students = db.students.find().sort('name',-1)
for student in students:
    print(student)

students = db.students.find().sort('age')
for student in students:
    print(student)

students = db.students.find().sort('age',-1)
for student in students:
    print(student)

app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

升序

```sh
{'_id': ObjectId('5df68a21f106fe2d315bbc8b'), 'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'age': 250}
{'_id': ObjectId('5df68a23f106fe2d315bbc8c'), 'name': 'David', 'country': 'UK', 'city': 'London', 'age': 34}
{'_id': ObjectId('5df68a23f106fe2d315bbc8d'), 'name': 'John', 'country': 'Sweden', 'city': 'Stockholm', 'age': 28}
{'_id': ObjectId('5df68a23f106fe2d315bbc8e'), 'name': 'Sami', 'country': 'Finland', 'city': 'Helsinki', 'age': 25}
```

降序

```sh
{'_id': ObjectId('5df68a23f106fe2d315bbc8e'), 'name': 'Sami', 'country': 'Finland', 'city': 'Helsinki', 'age': 25}
{'_id': ObjectId('5df68a23f106fe2d315bbc8d'), 'name': 'John', 'country': 'Sweden', 'city': 'Stockholm', 'age': 28}
{'_id': ObjectId('5df68a23f106fe2d315bbc8c'), 'name': 'David', 'country': 'UK', 'city': 'London', 'age': 34}
{'_id': ObjectId('5df68a21f106fe2d315bbc8b'), 'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'age': 250}
```

### 带查询条件的更新

我们将使用 *update_one()* 方法来更新一个条目。它接受两个对象，一个是查询对象，第二个是新对象。
第一个人 Asabeneh 的年龄非常不合理。让我们更新 Asabeneh 的年龄。

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
import pymongo

MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库

query = {'age':250}
new_value = {'$set':{'age':38}}

db.students.update_one(query, new_value)
# 让我们检查结果，看看年龄是否已修改
for student in db.students.find():
    print(student)


app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

```sh
{'_id': ObjectId('5df68a21f106fe2d315bbc8b'), 'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'age': 38}
{'_id': ObjectId('5df68a23f106fe2d315bbc8c'), 'name': 'David', 'country': 'UK', 'city': 'London', 'age': 34}
{'_id': ObjectId('5df68a23f106fe2d315bbc8d'), 'name': 'John', 'country': 'Sweden', 'city': 'Stockholm', 'age': 28}
{'_id': ObjectId('5df68a23f106fe2d315bbc8e'), 'name': 'Sami', 'country': 'Finland', 'city': 'Helsinki', 'age': 25}
```

当我们想要一次更新多个文档时，使用 *upate_many()* 方法。

### 删除文档

*delete_one()* 方法删除一个文档。*delete_one()* 接受一个查询对象参数。它只移除第一个匹配项。
让我们从集合中移除一个 John。

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
import pymongo

MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库

query = {'name':'John'}
db.students.delete_one(query)

for student in db.students.find():
    print(student)
# 让我们检查结果，看看年龄是否已修改
for student in db.students.find():
    print(student)


app = Flask(__name__)
if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

```sh
{'_id': ObjectId('5df68a21f106fe2d315bbc8b'), 'name': 'Asabeneh', 'country': 'Finland', 'city': 'Helsinki', 'age': 38}
{'_id': ObjectId('5df68a23f106fe2d315bbc8c'), 'name': 'David', 'country': 'UK', 'city': 'London', 'age': 34}
{'_id': ObjectId('5df68a23f106fe2d315bbc8e'), 'name': 'Sami', 'country': 'Finland', 'city': 'Helsinki', 'age': 25}
```

如你所见，John 已从集合中移除。

当我们想要删除多个文档时，使用 *delete_many()* 方法，它接受一个查询对象。如果我们将一个空查询对象传递给 *delete_many({})*，它将删除集合中的所有文档。

### 删除集合

使用 _drop()_ 方法，我们可以从数据库中删除一个集合。

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块
import pymongo

MONGODB_URI = 'mongodb+srv://asabeneh:your_password_goes_here@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库
db.students.drop()
```

现在，我们已经从数据库中删除了 students 集合。

## 💻 练习 - 第 27 天

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 26 天](../26_Day_Python_web/26_python_web_Python_Web开发.md) | [第 28 天 >>](../28_Day_API/28_API_API.md)
