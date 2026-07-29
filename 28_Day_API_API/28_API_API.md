<div align="center">
  <h1> 🐍 30 Days Of Python：第 28 天 - API</h1>
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

[<< 第 27 天](../27_Day_Python_with_mongodb_与MongoDB/27_python_with_mongodb_Python与MongoDB.md) | [第 29 天 >>](../29_Day_Building_API_构建API/29_building_API_构建API.md)

![30DaysOfPython](../images/30DaysOfPython_banner3@2x.png)

- [📘 第 28 天](#-第-28-天)
- [应用程序编程接口（API）](#应用程序编程接口api)
  - [API](#api)
  - [构建 API](#构建-api)
  - [HTTP（超文本传输协议）](#http超文本传输协议)
  - [HTTP 的结构](#http-的结构)
  - [初始请求行（状态行）](#初始请求行状态行)
    - [初始响应行（状态行）](#初始响应行状态行)
    - [头部字段](#头部字段)
    - [消息体](#消息体)
    - [请求方法](#请求方法)
  - [💻 练习 - 第 28 天](#-练习---第-28-天)

# 📘 第 28 天

# 应用程序编程接口（API）

## API

API 代表应用程序编程接口（Application Programming Interface）。本节将介绍的 API 类型是 Web API。
Web API 是定义的接口，企业和使用其资产的应用程序之间通过它进行交互，同时也是服务级别协议（SLA），用于指定功能提供者并为其 API 用户公开服务路径或 URL。

在 Web 开发的语境下，API 被定义为一组规范，例如超文本传输协议（HTTP）请求消息，以及响应消息的结构定义，通常采用 XML 或 JavaScript 对象表示法（JSON）格式。

Web API 正在从基于简单对象访问协议（SOAP）的 Web 服务和面向服务的架构（SOA）转向更直接的表述性状态转移（REST）风格的 Web 资源。

社交媒体服务中，Web API 允许 Web 社区在不同社区和平台之间共享内容和数据。

使用 API，在一个地方创建的内容可以动态地发布和更新到 Web 上的多个位置。

例如，Twitter 的 REST API 允许开发者访问 Twitter 核心数据，搜索 API（Search API）为开发者提供了与 Twitter Search 和趋势数据交互的方法。

许多应用程序提供 API 端点（end point）。一些 API 的示例，如国家[API](https://restcountries.eu/rest/v2/all)、[猫品种 API](https://api.thecatapi.com/v1/breeds)。

在本节中，我们将介绍一个使用 HTTP 请求方法来 GET、PUT、POST 和 DELETE 数据的 RESTful API。

## 构建 API

RESTful API 是一种应用程序编程接口（API），它使用 HTTP 请求来 GET、PUT、POST 和 DELETE 数据。在前面的章节中，我们已经学习了 python、flask 和 mongoDB。我们将使用所学的知识，用 Python flask 和 mongoDB 数据库开发一个 RESTful API。每个具有 CRUD（Create, Read, Update, Delete，即创建、读取、更新、删除）操作的应用程序都有一个 API 来创建数据、获取数据、更新数据或从数据库中删除数据。

要构建 API，最好理解 HTTP 协议以及 HTTP 请求和响应周期。

## HTTP（超文本传输协议）

HTTP 是客户端（client）和服务器（server）之间已建立的通信协议。在这个场景中，客户端是浏览器，服务器是你访问数据的地方。HTTP 是一种网络协议，用于传递资源，这些资源可以是万维网上的文件，无论是 HTML 文件、图像文件、查询结果、脚本还是其他文件类型。

浏览器是一个 HTTP 客户端，因为它向 HTTP 服务器（Web 服务器）发送请求，然后服务器向客户端返回响应。

## HTTP 的结构

HTTP 使用客户端-服务器模型。HTTP 客户端打开连接并向 HTTP 服务器发送请求消息，HTTP 服务器返回包含所请求资源的响应消息。当请求-响应周期完成后，服务器关闭连接。

![HTTP 请求-响应周期](../images/http_request_response_cycle.png)

请求和响应消息的格式相似。两种消息都具有：

- 一个初始行（initial line），
- 零个或多个头部行（header lines），
- 一个空行（即只有 CRLF 的行），以及
- 一个可选的消息体（例如文件、查询数据或查询输出）。

让我们通过访问这个站点来查看请求和响应消息的示例：https://thirtydaysofpython-v1-final.herokuapp.com/ 。该站点已部署在 Heroku 免费 dyno 上，由于请求量较大，几个月后可能无法访问。请支持这项工作以使服务器持续运行。

![请求和响应头](../images/request_response_header.png)

## 初始请求行（状态行）

初始请求行与响应行不同。
请求行由三部分组成，以空格分隔：

- 方法名（method name）（GET、POST、HEAD）
- 所请求资源的路径
- 正在使用的 HTTP 版本。例如 GET / HTTP/1.1

GET 是最常见的 HTTP 方法，用于获取或读取资源，POST 是用于创建资源的常见请求方法。

### 初始响应行（状态行）

初始响应行称为状态行（status line），也由三部分组成，以空格分隔：

- HTTP 版本
- 响应状态码（status code），给出请求结果，以及描述状态码的原因（reason）。状态行的示例：
  HTTP/1.0 200 OK
  或
  HTTP/1.0 404 Not Found
  注意：

最常见的状态码有：
200 OK：请求成功，结果资源（例如文件或脚本输出）在消息体中返回。
500 服务器错误（Server Error）
HTTP 状态码的完整列表可以在[这里](https://httpstatuses.com/)找到。也可以在[这里](https://httpstatusdogs.com/)找到。

### 头部字段

正如你在上面的截图中看到的，头部行提供关于请求或响应的信息，或关于消息体中发送的对象的信息。

```sh
GET / HTTP/1.1
Host: thirtydaysofpython-v1-final.herokuapp.com
Connection: keep-alive
Pragma: no-cache
Cache-Control: no-cache
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.79 Safari/537.36
Sec-Fetch-User: ?1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Referer: https://thirtydaysofpython-v1-final.herokuapp.com/post
Accept-Encoding: gzip, deflate, br
Accept-Language: en-GB,en;q=0.9,fi-FI;q=0.8,fi;q=0.7,en-CA;q=0.6,en-US;q=0.5,fr;q=0.4
```

### 消息体

HTTP 消息可能在头部行之后有一个数据体。在响应中，这是所请求资源返回给客户端的地方（消息体最常见的用途），或者在出错时可能是解释性文本。在请求中，这是用户输入的数据或上传的文件发送到服务器的地方。

如果 HTTP 消息包含一个消息体，消息中通常会有描述该消息体的头部行。特别是，

Content-Type: 头部给出消息体中数据的 MIME 类型（text/html、application/json、text/plain、text/css、image/gif）。
Content-Length: 头部给出消息体中的字节数。

### 请求方法

GET、POST、PUT 和 DELETE 是我们将要实现 API 或 CRUD 操作应用程序所使用的 HTTP 请求方法。

1. GET: GET 方法用于使用给定的 URI 从指定服务器检索（retrieve）和获取信息。使用 GET 的请求应该只检索数据，对数据不应有其他影响。

2. POST: POST 请求用于创建数据并将数据发送到服务器，例如，使用 HTML 表单创建新帖子、文件上传等。

3. PUT: 用上传的内容替换目标资源的所有当前表示，我们用它来修改或更新数据。

4. DELETE: 移除数据

## 💻 练习 - 第 28 天

1. 阅读关于 API 和 HTTP 的内容

🎉 恭喜（CONGRATULATIONS）！🎉

[<< 第 27 天](../27_Day_Python_with_mongodb_与MongoDB/27_python_with_mongodb_Python与MongoDB.md) | [第 29 天 >>](../29_Day_Building_API_构建API/29_building_API_构建API.md)
