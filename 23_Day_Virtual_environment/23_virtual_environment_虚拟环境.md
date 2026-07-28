<div align="center">
  <h1> 🐍 30 Days Of Python：第 23 天 - 虚拟环境（Virtual Environment）</h1>
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

[<< 第 22 天](../22_Day_Web_scraping/22_web_scraping_网络爬虫.md) | [第 24 天 >>](../24_Day_Statistics/24_statistics_统计学.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 23 天](#-第-23-天)
  - [设置虚拟环境](#设置虚拟环境)
  - [💻 练习 - 第 23 天](#-练习---第-23-天)

# 📘 第 23 天

## 设置虚拟环境

开始一个项目时，最好创建一个虚拟环境（virtual environment）。虚拟环境可以帮助我们创建一个隔离的或独立的环境。这将有助于我们避免跨项目的依赖（dependency）冲突。如果你在终端上输入 pip freeze，你会看到计算机上所有已安装的包（package）。如果我们使用 virtualenv，我们将只能访问特定于该项目的包。打开你的终端并安装 virtualenv

```sh
asabeneh@Asabeneh:~$ pip install virtualenv
```

在 30DaysOfPython 文件夹内创建一个 flask_project 文件夹。

安装 virtualenv 包后，进入你的项目文件夹并通过以下命令创建虚拟环境：

对于 Mac/Linux：
```sh
asabeneh@Asabeneh:~/Desktop/30DaysOfPython/flask_project\$ virtualenv venv

```

对于 Windows：
```sh
C:\Users\User\Documents\30DaysOfPython\flask_project>python -m venv venv
```

我喜欢将新项目称为 venv，但你可以随意命名。让我们使用 ls（或 Windows 命令提示符的 dir）命令检查 venv 是否已创建。

```sh
asabeneh@Asabeneh:~/Desktop/30DaysOfPython/flask_project$ ls
venv/
```

让我们通过在项目文件夹中输入以下命令来激活虚拟环境。

对于 Mac/Linux：
```sh
asabeneh@Asabeneh:~/Desktop/30DaysOfPython/flask_project$ source venv/bin/activate
```
在 Windows 上，虚拟环境的激活在 Windows Power shell 和 git bash 中可能有所不同。

对于 Windows Power Shell：
```sh
C:\Users\User\Documents\30DaysOfPython\flask_project> venv\Scripts\activate
```

对于 Windows Git bash：
```sh
C:\Users\User\Documents\30DaysOfPython\flask_project> venv\Scripts\. activate
```

输入激活命令后，你的项目目录将以 venv 开头。请参见下面的示例。

```sh
(venv) asabeneh@Asabeneh:~/Desktop/30DaysOfPython/flask_project$
```

现在，让我们通过输入 pip freeze 来检查此项目中可用的包。你不会看到任何包。

我们将做一个小的 flask 项目，所以让我们为这个项目安装 flask 包。

```sh
(venv) asabeneh@Asabeneh:~/Desktop/30DaysOfPython/flask_project$ pip install Flask
```

现在，让我们输入 pip freeze 来查看项目中已安装包的列表：

```sh
(venv) asabeneh@Asabeneh:~/Desktop/30DaysOfPython/flask_project$ pip freeze
Click==7.0
Flask==1.1.1
itsdangerous==1.1.0
Jinja2==2.10.3
MarkupSafe==1.1.1
Werkzeug==0.16.0
```

完成后，你应该使用 _deactivate_ 来停用（deactivate）活动项目。

```sh
(venv) asabeneh@Asabeneh:~/Desktop/30DaysOfPython$ deactivate
```

使用 flask 所需的模块（module）已安装。现在，你的项目目录已准备好进行 flask 项目。你应该将 venv 添加到你的 .gitignore 文件中，以免将其推送到 github。

## 💻 练习 - 第 23 天

1. 根据上面给出的示例，创建一个带有虚拟环境的项目目录。

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 22 天](../22_Day_Web_scraping/22_web_scraping_网络爬虫.md) | [第 24 天 >>](../24_Day_Statistics/24_statistics_统计学.md)
