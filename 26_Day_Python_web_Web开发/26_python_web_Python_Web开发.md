<div align="center">
  <h1> 🐍 30 Days Of Python：第 26 天 - Python Web 开发</h1>
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

[<< 第 25 天](../25_Day_Pandas_Pandas/25_pandas_Pandas.md) | [第 27 天 >>](../27_Day_Python_with_mongodb_与MongoDB/27_python_with_mongodb_Python与MongoDB.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 26 天](#-第-26-天)
  - [Python Web 开发](#python-web-开发)
    - [Flask](#flask)
      - [文件夹结构](#文件夹结构)
    - [设置项目目录](#设置项目目录)
    - [创建路由](#创建路由)
    - [创建模板](#创建模板)
    - [Python 脚本](#python-脚本)
    - [导航](#导航)
    - [创建布局](#创建布局)
      - [提供静态文件](#提供静态文件)
    - [部署](#部署)
      - [创建 Heroku 账号](#创建-heroku-账号)
      - [登录 Heroku](#登录-heroku)
      - [创建 requirements 和 Procfile](#创建-requirements-和-procfile)
      - [将项目推送到 heroku](#将项目推送到-heroku)
  - [💻 练习 - 第 26 天](#-练习---第-26-天)

# 📘 第 26 天

## Python Web 开发

Python 是一种通用编程语言，它可以用于许多领域。在本节中，我们将看到如何将 Python 用于 Web 开发。有许多 Python Web 框架（framework）。Django 和 Flask 是最流行的两个。今天，我们将了解如何使用 Flask 进行 Web 开发。

### Flask

Flask 是一个用 Python 编写的 Web 开发框架。Flask 使用 Jinja2 模板引擎（template engine）。Flask 也可以与其他现代前端库（front library）如 React 配合使用。

如果你还没有安装 virtualenv 包，请先安装它。虚拟环境（Virtual environment）可以将项目依赖与本地机器的依赖隔离开来。

#### 文件夹结构

完成所有步骤后，你的项目文件结构应该如下所示：

```sh

├── Procfile
├── app.py
├── env
│   ├── bin
├── requirements.txt
├── static
│   └── css
│       └── main.css
└── templates
    ├── about.html
    ├── home.html
    ├── layout.html
    ├── post.html
    └── result.html
```

### 设置项目目录

按照以下步骤开始使用 Flask。

第 1 步：使用以下命令安装 virtualenv。

```sh
pip install virtualenv
```

第 2 步：

```sh
asabeneh@Asabeneh:~/Desktop$ mkdir python_for_web
asabeneh@Asabeneh:~/Desktop$ cd python_for_web/
asabeneh@Asabeneh:~/Desktop/python_for_web$ virtualenv venv
asabeneh@Asabeneh:~/Desktop/python_for_web$ source venv/bin/activate
(env) asabeneh@Asabeneh:~/Desktop/python_for_web$ pip freeze
(env) asabeneh@Asabeneh:~/Desktop/python_for_web$ pip install Flask
(env) asabeneh@Asabeneh:~/Desktop/python_for_web$ pip freeze
Click==7.0
Flask==1.1.1
itsdangerous==1.1.0
Jinja2==2.10.3
MarkupSafe==1.1.1
Werkzeug==0.16.0
(env) asabeneh@Asabeneh:~/Desktop/python_for_web$
```

我们创建了一个名为 python_for_web 的项目目录。在项目内部，我们创建了一个名为 *venv* 的虚拟环境（可以是任意名称，但我更倾向于叫它 _venv_）。然后我们激活了虚拟环境。我们使用 pip freeze 来检查项目目录中已安装的包。pip freeze 的结果是空的，因为尚未安装任何包。

现在，让我们在项目目录中创建 app.py 文件并编写以下代码。app.py 文件将是项目中的主文件。以下代码包含 flask 模块和 os 模块。

### 创建路由

主页路由（home route）。

```py
# 导入 flask
from flask import Flask
import os # 导入操作系统模块

app = Flask(__name__)

@app.route('/') # 这个装饰器（decorator）创建主页路由
def home ():
    return '<h1>Welcome</h1>'

if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

要运行 Flask 应用程序，请在主 Flask 应用程序目录中输入 python app.py。

运行 _python app.py_ 后，请检查本地主机（local host）5000 端口。

让我们添加额外的路由。
创建 about 路由

```py
# 导入 flask
from flask import Flask
import os # 导入操作系统模块

app = Flask(__name__)

@app.route('/') # 这个装饰器创建主页路由
def home ():
    return '<h1>Welcome</h1>'

@app.route('/about')
def about():
    return '<h1>About us</h1>'

if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

现在，我们在上面的代码中添加了 about 路由。如果我们想渲染（render）一个 HTML 文件而不是字符串，该怎么办？可以使用 *render_template* 函数来渲染 HTML 文件。让我们创建一个名为 templates 的文件夹，并在项目目录中创建 home.html 和 about.html。同时从 flask 导入 *render_template* 函数。

### 创建模板

在 templates 文件夹内创建 HTML 文件。

home.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Home</title>
  </head>

  <body>
    <h1>Welcome Home</h1>
  </body>
</html>
```

about.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>About</title>
  </head>

  <body>
    <h1>About Us</h1>
  </body>
</html>
```

### Python 脚本

app.py

```py
# 导入 flask
from flask import Flask, render_template
import os # 导入操作系统模块

app = Flask(__name__)

@app.route('/') # 这个装饰器创建主页路由
def home ():
    return render_template('home.html')

@app.route('/about')
def about():
    return render_template('about.html')

if __name__ == '__main__':
    # 为了部署，我们使用 environ
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

如你所见，要跳转到不同页面或进行导航，我们需要一个导航。让我们为每个页面添加链接，或者创建一个用于每个页面的布局（layout）。

### 导航

```html
<ul>
  <li><a href="/">Home</a></li>
  <li><a href="/about">About</a></li>
</ul>
```

现在，我们可以使用上面的链接在页面之间导航。让我们创建一个处理表单数据（form data）的附加页面。你可以叫它任何名字，我喜欢叫它 post.html。

我们可以使用 Jinja2 模板引擎将数据注入（inject）到 HTML 文件中。

```py
# 导入 flask
from flask import Flask, render_template, request, redirect, url_for
import os # 导入操作系统模块

app = Flask(__name__)

@app.route('/') # 这个装饰器创建主页路由
def home ():
    techs = ['HTML', 'CSS', 'Flask', 'Python']
    name = '30 Days Of Python Programming'
    return render_template('home.html', techs=techs, name = name, title = 'Home')

@app.route('/about')
def about():
    name = '30 Days Of Python Programming'
    return render_template('about.html', name = name, title = 'About Us')

@app.route('/post')
def post():
    name = 'Text Analyzer'
    return render_template('post.html', name = name, title = name)


if __name__ == '__main__':
    # 为了部署
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

让我们也看看模板：

home.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Home</title>
  </head>

  <body>
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/about">About</a></li>
    </ul>
    <h1>Welcome to {{name}}</h1>
     <ul>
    {% for tech in techs %}
      <li>{{tech}}</li>
    {% endfor %}
    </ul>
  </body>
</html>
```

about.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>About Us</title>
  </head>

  <body>
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/about">About</a></li>
    </ul>
    <h1>About Us</h1>
    <h2>{{name}}</h2>
  </body>
</html>
```

### 创建布局

在模板文件中，有许多重复的代码，我们可以编写一个布局来消除重复。让我们在 templates 文件夹内创建 layout.html。
创建布局后，我们将其导入到每个文件中。

#### 提供静态文件

在你的项目目录中创建一个 static 文件夹。在 static 文件夹内创建 CSS 或 styles 文件夹，并创建一个 CSS 样式表。我们使用 *url_for* 模块来提供静态文件。

layout.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      href="https://fonts.googleapis.com/css?family=Lato:300,400|Nunito:300,400|Raleway:300,400,500&display=swap"
      rel="stylesheet"
    />
    <link
      rel="stylesheet"
      href="{{ url_for('static', filename='css/main.css') }}"
    />
    {% if title %}
    <title>30 Days of Python - {{ title}}</title>
    {% else %}
    <title>30 Days of Python</title>
    {% endif %}
  </head>

  <body>
    <header>
      <div class="menu-container">
        <div>
          <a class="brand-name nav-link" href="/">30DaysOfPython</a>
        </div>
        <ul class="nav-lists">
          <li class="nav-list">
            <a class="nav-link active" href="{{ url_for('home') }}">Home</a>
          </li>
          <li class="nav-list">
            <a class="nav-link active" href="{{ url_for('about') }}">About</a>
          </li>
          <li class="nav-list">
            <a class="nav-link active" href="{{ url_for('post') }}"
              >Text Analyzer</a
            >
          </li>
        </ul>
      </div>
    </header>
    <main>
      {% block content %} {% endblock %}
    </main>
  </body>
</html>
```

现在，让我们移除其他模板文件中所有重复的代码并导入 layout.html。href 使用 _url_for_ 函数配合路由函数的名称来连接每个导航路由。

home.html

```html
{% extends 'layout.html' %} {% block content %}
<div class="container">
  <h1>Welcome to {{name}}</h1>
  <p>
    This application clean texts and analyse the number of word, characters and
    most frequent words in the text. Check it out by click text analyzer at the
    menu. You need the following technologies to build this web application:
  </p>
  <ul class="tech-lists">
    {% for tech in techs %}
    <li class="tech">{{tech}}</li>

    {% endfor %}
  </ul>
</div>

{% endblock %}
```

about.html

```html
{% extends 'layout.html' %} {% block content %}
<div class="container">
  <h1>About {{name}}</h1>
  <p>
    This is a 30 days of python programming challenge. If you have been coding
    this far, you are awesome. Congratulations for the job well done!
  </p>
</div>
{% endblock %}
```

post.html

```html
{% extends 'layout.html' %} {% block content %}
<div class="container">
  <h1>Text Analyzer</h1>
  <form action="https://thirtydaysofpython-v1.herokuapp.com/post" method="POST">
    <div>
      <textarea rows="25" name="content" autofocus></textarea>
    </div>
    <div>
      <input type="submit" class="btn" value="Process Text" />
    </div>
  </form>
</div>

{% endblock %}
```

请求方法（Request methods），有不同的请求方法（GET、POST、PUT、DELETE），它们是允许我们执行 CRUD（Create, Read, Update, Delete，即创建、读取、更新、删除）操作的常见请求方法。

在 post 路由中，我们将根据请求类型交替使用 GET 和 POST 方法，请查看下面的代码。请求方法是一个用于处理请求方法以及访问表单数据的函数。
app.py

```py
# 导入 flask
from flask import Flask, render_template, request, redirect, url_for
import os # 导入操作系统模块

app = Flask(__name__)
# 阻止静态文件缓存
app.config['SEND_FILE_MAX_AGE_DEFAULT'] = 0



@app.route('/') # 这个装饰器创建主页路由
def home ():
    techs = ['HTML', 'CSS', 'Flask', 'Python']
    name = '30 Days Of Python Programming'
    return render_template('home.html', techs=techs, name = name, title = 'Home')

@app.route('/about')
def about():
    name = '30 Days Of Python Programming'
    return render_template('about.html', name = name, title = 'About Us')

@app.route('/result')
def result():
    return render_template('result.html')

@app.route('/post', methods= ['GET','POST'])
def post():
    name = 'Text Analyzer'
    if request.method == 'GET':
         return render_template('post.html', name = name, title = name)
    if request.method =='POST':
        content = request.form['content']
        print(content)
        return redirect(url_for('result'))

if __name__ == '__main__':
    # 为了部署
    # 让它同时适用于生产环境和开发环境
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
```

到目前为止，我们已经了解了如何使用模板、如何向模板注入数据，以及如何创建通用布局。
现在，让我们处理静态文件。在项目目录中创建一个名为 static 的文件夹，再创建一个名为 css 的文件夹。在 css 文件夹内创建 main.css。你的 main.css 文件将被链接到 layout.html。

你不必自己编写 css 文件，复制并使用即可。让我们继续部署。

### 部署

#### 创建 Heroku 账号

Heroku 为前端和全栈（fullstack）应用程序提供免费的部署服务。请在 [heroku](https://www.heroku.com/) 上创建一个账号，并为你的机器安装 Heroku [CLI](https://devcenter.heroku.com/articles/heroku-cli)。
安装 heroku 后，输入以下命令

#### 登录 Heroku

```sh
asabeneh@Asabeneh:~$ heroku login
heroku: Press any key to open up the browser to login or q to exit:
```

让我们通过点击键盘上的任意键来查看结果。当你按下键盘上的任意键时，它将打开 heroku 登录页面，点击登录页面。然后你的本地机器将连接到远程 heroku 服务器。如果你已连接到远程服务器，你将看到以下内容。

```sh
asabeneh@Asabeneh:~$ heroku login
heroku: Press any key to open up the browser to login or q to exit:
Opening browser to https://cli-auth.heroku.com/auth/browser/be12987c-583a-4458-a2c2-ba2ce7f41610
Logging in... done
Logged in as asabeneh@gmail.com
asabeneh@Asabeneh:~$
```

#### 创建 requirements 和 Procfile

在我们将代码推送到远程服务器之前，需要准备以下内容：

- requirements.txt
- Procfile

```sh
(env) asabeneh@Asabeneh:~/Desktop/python_for_web$ pip freeze
Click==7.0
Flask==1.1.1
itsdangerous==1.1.0
Jinja2==2.10.3
MarkupSafe==1.1.1
Werkzeug==0.16.0
(env) asabeneh@Asabeneh:~/Desktop/python_for_web$ touch requirements.txt
(env) asabeneh@Asabeneh:~/Desktop/python_for_web$ pip freeze > requirements.txt
(env) asabeneh@Asabeneh:~/Desktop/python_for_web$ cat requirements.txt
Click==7.0
Flask==1.1.1
itsdangerous==1.1.0
Jinja2==2.10.3
MarkupSafe==1.1.1
Werkzeug==0.16.0
(env) asabeneh@Asabeneh:~/Desktop/python_for_web$ touch Procfile
(env) asabeneh@Asabeneh:~/Desktop/python_for_web$ ls
Procfile          env/              static/
app.py            requirements.txt  templates/
(env) asabeneh@Asabeneh:~/Desktop/python_for_web$
```

Procfile 将包含在 Web 服务器中运行应用程序的命令，在我们的例子中是在 Heroku 上。

```sh
web: python app.py
```

#### 将项目推送到 heroku

现在，已准备好进行部署。在 heroku 上部署应用程序的步骤：

1. git init
2. git add .
3. git commit -m "commit message"
4. heroku create 'name of the app as one word'
5. git push heroku master
6. heroku open（启动已部署的应用程序）

完成此步骤后，你将获得一个类似[这样](http://thirdaysofpython-practice.herokuapp.com/)的应用程序。

## 💻 练习 - 第 26 天

1. 你将构建[这个应用程序](https://thirtydaysofpython-v1-final.herokuapp.com/)。只剩下文本分析器（text analyser）部分。


🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 25 天](../25_Day_Pandas_Pandas/25_pandas_Pandas.md) | [第 27 天 >>](../27_Day_Python_with_mongodb_与MongoDB/27_python_with_mongodb_Python与MongoDB.md)
