<div align="center">
  <h1> 🐍 30 Days Of Python：第 29 天 - 构建 API</h1>
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

[<< 第 28 天](../28_Day_API/28_API_API.md) | [第 30 天 >>](../30_Day_Conclusions/30_conclusions_总结.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [第 29 天](#第-29-天)
- [构建 API](#构建-api)
  - [API 的结构](#api-的结构)
  - [使用 GET 检索数据](#使用-get-检索数据)
  - [通过 id 获取文档](#通过-id-获取文档)
  - [使用 POST 创建数据](#使用-post-创建数据)
  - [使用 PUT 更新](#使用-put-更新)
  - [使用 DELETE 删除文档](#使用-delete-删除文档)
- [💻 练习 - 第 29 天](#-练习---第-29-天)

## 第 29 天

## 构建 API

在本节中，我们将介绍一个使用 HTTP 请求方法来 GET、PUT、POST 和 DELETE 数据的 RESTful API。

RESTful API 是一种应用程序编程接口（API），它使用 HTTP 请求来 GET、PUT、POST 和 DELETE 数据。在前面的章节中，我们已经学习了 python、flask 和 mongoDB。我们将使用所学的知识，用 python flask 和 mongoDB 构建一个 RESTful API。每个具有 CRUD（Create, Read, Update, Delete，即创建、读取、更新、删除）操作的应用程序都有一个 API 来创建数据、获取数据、更新数据或从数据库中删除数据。

浏览器只能处理 GET 请求。因此，我们需要一个工具来帮助我们处理所有请求方法（GET、POST、PUT、DELETE）。

API 示例

- 国家 API：https://restcountries.eu/rest/v2/all
- 猫品种 API：https://api.thecatapi.com/v1/breeds

[Postman](https://www.getpostman.com/) 是 API 开发中非常流行的工具。因此，如果你想学习本节内容，需要[下载 postman](https://www.getpostman.com/)。Postman 的替代工具是 [Insomnia](https://insomnia.rest/download)。

![Postman](../images/postman.png)

### API 的结构

API 端点（end point）是一个 URL，它可以帮助检索、创建、更新或删除资源。结构如下所示：
示例：
https://api.twitter.com/1.1/lists/members.json
返回指定列表的成员。仅当经过身份验证的用户拥有指定列表时，才会显示私有列表成员。
公司名称后跟版本号，再跟 API 的用途。
方法：
HTTP 方法和 URL

API 使用以下 HTTP 方法进行对象操作：

```sh
GET        用于对象检索
POST       用于对象创建和对象操作
PUT        用于对象更新
DELETE     用于对象删除
```

让我们构建一个收集 30DaysOfPython 学生信息的 API。我们将收集姓名、国家、城市、出生日期、技能（skills）和个人简介（bio）。

为了实现这个 API，我们将使用：

- Postman
- Python
- Flask
- MongoDB

### 使用 GET 检索数据

在这一步中，让我们使用虚拟数据（dummy data）并将其作为 json 返回。为了将其作为 json 返回，我们将使用 json 模块和 Response 模块。

```py
# 导入 flask

from flask import Flask,  Response
import json
import os

app = Flask(__name__)

@app.route('/api/v1.0/students', methods = ['GET'])
def students ():
    student_list = [
        {
            'name':'Asabeneh',
            'country':'Finland',
            'city':'Helsinki',
            'skills':['HTML', 'CSS','JavaScript','Python']
        },
        {
            'name':'David',
            'country':'UK',
            'city':'London',
            'skills':['Python','MongoDB']
        },
        {
            'name':'John',
            'country':'Sweden',
            'city':'Stockholm',
            'skills':['Java','C#']
        }
    ]
    return Response(json.dumps(student_list), mimetype='application/json')


if __name__ == '__main__':
    # 为了部署
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

当你在浏览器中请求 http://localhost:5000/api/v1.0/students 这个 URL 时，你会得到以下结果：

![在浏览器中 GET](../images/get_on_browser.png)

当你在浏览器中请求 http://localhost:5000/api/v1.0/students 这个 URL 时，你会得到以下结果：

![在 Postman 中 GET](../images/get_on_postman.png)

让我们不再显示虚拟数据，而是将 flask 应用程序与 MongoDB 连接，从 mongoDB 数据库获取数据。

```py
# 导入 flask

from flask import Flask,  Response
import json
import pymongo
import os

app = Flask(__name__)

#
MONGODB_URI='mongodb+srv://asabeneh:your_password@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库

@app.route('/api/v1.0/students', methods = ['GET'])
def students ():

    return Response(json.dumps(student), mimetype='application/json')


if __name__ == '__main__':
    # 为了部署
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

通过连接 flask，我们可以从 thirty_days_of_python 数据库中获取 students 集合的数据。

```sh
[
    {
        "_id": {
            "$oid": "5df68a21f106fe2d315bbc8b"
        },
        "name": "Asabeneh",
        "country": "Finland",
        "city": "Helsinki",
        "age": 38
    },
    {
        "_id": {
            "$oid": "5df68a23f106fe2d315bbc8c"
        },
        "name": "David",
        "country": "UK",
        "city": "London",
        "age": 34
    },
    {
        "_id": {
            "$oid": "5df68a23f106fe2d315bbc8e"
        },
        "name": "Sami",
        "country": "Finland",
        "city": "Helsinki",
        "age": 25
    }
]
```

### 通过 id 获取文档

我们可以通过 id 访问单个文档，让我们通过他的 id 访问 Asabeneh。
http://localhost:5000/api/v1.0/students/5df68a21f106fe2d315bbc8b

```py
# 导入 flask

from flask import Flask,  Response
import json
from bson.objectid import ObjectId
import json
from bson.json_util import dumps
import pymongo
import os

app = Flask(__name__)

#
MONGODB_URI='mongodb+srv://asabeneh:your_password@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库

@app.route('/api/v1.0/students', methods = ['GET'])
def students ():

    return Response(json.dumps(student), mimetype='application/json')
@app.route('/api/v1.0/students/<id>', methods = ['GET'])
def single_student (id):
    student = db.students.find({'_id':ObjectId(id)})
    return Response(dumps(student), mimetype='application/json')

if __name__ == '__main__':
    # 为了部署
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

```sh
[
    {
        "_id": {
            "$oid": "5df68a21f106fe2d315bbc8b"
        },
        "name": "Asabeneh",
        "country": "Finland",
        "city": "Helsinki",
        "age": 38
    }
]
```

### 使用 POST 创建数据

我们使用 POST 请求方法来创建数据

```py
# 导入 flask

from flask import Flask,  Response
import json
from bson.objectid import ObjectId
import json
from bson.json_util import dumps
import pymongo
from datetime import datetime
import os

app = Flask(__name__)

#
MONGODB_URI='mongodb+srv://asabeneh:your_password@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库

@app.route('/api/v1.0/students', methods = ['GET'])
def students ():

    return Response(json.dumps(student), mimetype='application/json')
@app.route('/api/v1.0/students/<id>', methods = ['GET'])
def single_student (id):
    student = db.students.find({'_id':ObjectId(id)})
    return Response(dumps(student), mimetype='application/json')
@app.route('/api/v1.0/students', methods = ['POST'])
def create_student ():
    name = request.form['name']
    country = request.form['country']
    city = request.form['city']
    skills = request.form['skills'].split(', ')
    bio = request.form['bio']
    birthyear = request.form['birthyear']
    created_at = datetime.now()
    student = {
        'name': name,
        'country': country,
        'city': city,
        'birthyear': birthyear,
        'skills': skills,
        'bio': bio,
        'created_at': created_at

    }
    db.students.insert_one(student)
    return ;
def update_student (id):
if __name__ == '__main__':
    # 为了部署
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

### 使用 PUT 更新

```py
# 导入 flask

from flask import Flask,  Response
import json
from bson.objectid import ObjectId
import json
from bson.json_util import dumps
import pymongo
from datetime import datetime
import os

app = Flask(__name__)

#
MONGODB_URI='mongodb+srv://asabeneh:your_password@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库

@app.route('/api/v1.0/students', methods = ['GET'])
def students ():

    return Response(json.dumps(student), mimetype='application/json')
@app.route('/api/v1.0/students/<id>', methods = ['GET'])
def single_student (id):
    student = db.students.find({'_id':ObjectId(id)})
    return Response(dumps(student), mimetype='application/json')
@app.route('/api/v1.0/students', methods = ['POST'])
def create_student ():
    name = request.form['name']
    country = request.form['country']
    city = request.form['city']
    skills = request.form['skills'].split(', ')
    bio = request.form['bio']
    birthyear = request.form['birthyear']
    created_at = datetime.now()
    student = {
        'name': name,
        'country': country,
        'city': city,
        'birthyear': birthyear,
        'skills': skills,
        'bio': bio,
        'created_at': created_at

    }
    db.students.insert_one(student)
    return
@app.route('/api/v1.0/students/<id>', methods = ['PUT']) # 这个装饰器创建主页路由
def update_student (id):
    query = {"_id":ObjectId(id)}
    name = request.form['name']
    country = request.form['country']
    city = request.form['city']
    skills = request.form['skills'].split(', ')
    bio = request.form['bio']
    birthyear = request.form['birthyear']
    created_at = datetime.now()
    student = {
        'name': name,
        'country': country,
        'city': city,
        'birthyear': birthyear,
        'skills': skills,
        'bio': bio,
        'created_at': created_at

    }
    db.students.update_one(query, student)
    # return Response(dumps({"result":"a new student has been created"}), mimetype='application/json')
    return
def update_student (id):
if __name__ == '__main__':
    # 为了部署
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

### 使用 DELETE 删除文档

```py
# 导入 flask

from flask import Flask,  Response
import json
from bson.objectid import ObjectId
import json
from bson.json_util import dumps
import pymongo
from datetime import datetime
import os

app = Flask(__name__)

#
MONGODB_URI='mongodb+srv://asabeneh:your_password@30daysofpython-twxkr.mongodb.net/test?retryWrites=true&w=majority'
client = pymongo.MongoClient(MONGODB_URI)
db = client['thirty_days_of_python'] # 访问数据库

@app.route('/api/v1.0/students', methods = ['GET'])
def students ():

    return Response(json.dumps(student), mimetype='application/json')
@app.route('/api/v1.0/students/<id>', methods = ['GET'])
def single_student (id):
    student = db.students.find({'_id':ObjectId(id)})
    return Response(dumps(student), mimetype='application/json')
@app.route('/api/v1.0/students', methods = ['POST'])
def create_student ():
    name = request.form['name']
    country = request.form['country']
    city = request.form['city']
    skills = request.form['skills'].split(', ')
    bio = request.form['bio']
    birthyear = request.form['birthyear']
    created_at = datetime.now()
    student = {
        'name': name,
        'country': country,
        'city': city,
        'birthyear': birthyear,
        'skills': skills,
        'bio': bio,
        'created_at': created_at

    }
    db.students.insert_one(student)
    return
@app.route('/api/v1.0/students/<id>', methods = ['PUT']) # 这个装饰器创建主页路由
def update_student (id):
    query = {"_id":ObjectId(id)}
    name = request.form['name']
    country = request.form['country']
    city = request.form['city']
    skills = request.form['skills'].split(', ')
    bio = request.form['bio']
    birthyear = request.form['birthyear']
    created_at = datetime.now()
    student = {
        'name': name,
        'country': country,
        'city': city,
        'birthyear': birthyear,
        'skills': skills,
        'bio': bio,
        'created_at': created_at

    }
    db.students.update_one(query, student)
    # return Response(dumps({"result":"a new student has been created"}), mimetype='application/json')
    return
@app.route('/api/v1.0/students/<id>', methods = ['PUT']) # 这个装饰器创建主页路由
def update_student (id):
    query = {"_id":ObjectId(id)}
    name = request.form['name']
    country = request.form['country']
    city = request.form['city']
    skills = request.form['skills'].split(', ')
    bio = request.form['bio']
    birthyear = request.form['birthyear']
    created_at = datetime.now()
    student = {
        'name': name,
        'country': country,
        'city': city,
        'birthyear': birthyear,
        'skills': skills,
        'bio': bio,
        'created_at': created_at

    }
    db.students.update_one(query, student)
    # return Response(dumps({"result":"a new student has been created"}), mimetype='application/json')
    return ;
@app.route('/api/v1.0/students/<id>', methods = ['DELETE'])
def delete_student (id):
    db.students.delete_one({"_id":ObjectId(id)})
    return
if __name__ == '__main__':
    # 为了部署
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

## 💻 练习 - 第 29 天

1. 实现上面的示例并开发[这个](https://thirtydayofpython-api.herokuapp.com/)

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 28 天](../28_Day_API/28_API_API.md) | [第 30 天 >>](../30_Day_Conclusions/30_conclusions_总结.md)
