# pytest 自动化测试框架与常用附带工具全景使用指南

本指南整合了 pytest 框架的核心规范、前后置夹具系统（Fixture）、测试标记（Mark）、数据驱动（DDT）、Faker 随机测试数据库以及 Allure 报表生成等高级特性，旨在提供一份结构完整、案例详实、可直接应用于企业级项目实战的 pytest 自动化测试笔记。

---

## 目录
1. [pytest 框架基本规范与执行方式](#1-pytest-框架基本规范与执行方式)
   - 1.1 [文件目录与命名规范](#11-文件目录与命名规范)
   - 1.2 [用例执行机制](#12-用例执行机制)
2. [用例前后置处理 (Setup & Teardown)](#2-用例前后置处理-setup--teardown)
   - 2.1 [传统 xUnit 风格前后置](#21-传统-xunit-风格前后置)
   - 2.2 [现代 fixture + conftest 夹具系统](#22-现代-fixture--conftest-夹具系统)
3. [pytest 高级功能与标记应用](#3-pytest-高级功能与标记应用)
   - 3.1 [mark 标记的核心应用](#31-mark-标记的核心应用)
   - 3.2 [装饰器装配与运行执行顺序 (洋葱模型)](#32-装饰器装配与运行执行顺序-洋葱模型)
4. [数据驱动测试 (DDT)](#4-数据驱动测试-ddt)
   - 4.1 [JSON 数据读取](#41-json-数据读取)
   - 4.2 [参数化用例实现](#42-参数化用例实现)
5. [Faker 随机测试数据库](#5-faker-随机测试数据库)
6. [Allure 专业测试报告集成](#6-allure-专业测试报告集成)
   - 6.1 [环境搭建与 ini 配置](#61-环境搭建与-ini-配置)
   - 6.2 [在线报告与离线 HTML 报告生成](#62-在线报告与离线-html-报告生成)

---

## 1. pytest 框架基本规范与执行方式

### 1.1 文件目录与命名规范

在企业级自动化测试中，规范的文件目录结构和命名标准可以保证项目的可维护性与框架的自动识别效率。通常的目录设计规范如下：

```text
ProjectRoot/
├── api/                  # 存放各种接口封装/业务接口操作方法包
│   └── order_api.py
├── scripts/              # 存放测试用例脚本包
│   └── test_order.py
├── data/                 # 存放测试数据（如 JSON, YAML 等）
│   └── order_data.json
├── tools/                # 存放工具类方法（如数据读取、日志记录等）
│   └── read_json.py
├── conftest.py          # 全局夹具配置
├── pytest.ini            # pytest 核心配置文件
└── cmd_allure.py         # 离线 Allure 报表生成辅助脚本
```

#### 命名规范细则：
* **测试文件**：必须以 `test_` 开头（或以 `_test` 结尾），例如 `test_login.py`、`test_01_order.py`。
* **测试类名**：必须以 `Test` 开头，且不能含有 `__init__` 初始化方法，例如 `TestLogin`。
* **测试方法/用例名**：必须以 `test_` 开头，推荐命名格式为 `test_编号_操作_场景`，例如 `test_01_login_success`。

---

### 1.2 用例执行机制

#### 1.2.1 单用例运行方式
在调试阶段，我们常常需要单独执行某一个文件、某一个类，甚至是类中的某一个具体测试方法。

* **命令行运行方式**：
  ```bash
  # 运行整个文件
  pytest -s test_login.py
  
  # 运行指定文件下的指定测试类
  pytest -s test_login.py::TestLogin
  
  # 运行指定类中的具体测试方法
  pytest -s test_login.py::TestLogin::test_01_login_success
  ```
  *(注：`-s` 参数表示禁用输出捕获，允许将代码中的 `print` 输出或日志直接打印在控制台上)*

* **Python 入口运行方式**：
  在测试脚本的末尾添加 `main` 方法，通过运行 Python 文件来启动：
  ```python
  import pytest

  if __name__ == '__main__':
      # 等同于在命令行中执行: pytest -s test_login.py
      pytest.main(['-s', 'test_login.py'])
  ```

#### 1.2.2 批量运行配置：`pytest.ini` 配置文件
对于大规模用例的自动化执行，不推荐每次都输入复杂的命令行参数，而是应当在项目根目录下创建统一的配置文件 `pytest.ini`：

```ini
[pytest]
# addopts: 配置 pytest 运行时的默认附加命令行参数
#   -s                 : 允许在控制台打印 stdout 输出
#   --alluredir        : 指定 Allure 报告原始数据的存储目录
#   --clean-alluredir   : 每次运行前清空旧的 Allure 报告原始数据目录
addopts = -s --alluredir ./report --clean-alluredir

# testpaths: 指定测试用例的搜索根路径
testpaths = ./scripts

# python_files: 指定测试用例文件的匹配规则
python_files = test*.py

# python_classes: 指定测试类的匹配规则
python_classes = Test*

# python_functions: 指定测试方法的匹配规则
python_functions = test*

# markers: 声明自定义测试标记，避免运行时抛出不规范标记的 Warning 警告
markers =
    smoke: 冒烟测试
    regression: 回归测试
```

---

## 2. 用例前后置处理 (Setup & Teardown)

pytest 提供了两种处理测试用例前置准备和后置清理的机制：**传统类 xUnit 风格的前置** 与 **现代 pytest 特有的 fixture 夹具系统**。

### 2.1 传统 xUnit 风格前后置

传统的前后置方法名字固定，根据不同的作用域，主要分为类层级、方法层级和模块层级。

```python
class TestDemo:
    
    # 1. 类级别：在当前测试类中所有用例执行前后各运行一次（必须是类方法）
    def setup_class(self):
        print("\n--- 类级别前置：[setup_class] 数据库连接或驱动初始化 ---")
        
    def teardown_class(self):
        print("\n--- 类级别后置：[teardown_class] 关闭数据库连接或销毁驱动 ---")

    # 2. 方法级别：类中每一个测试用例执行前后都会运行一次
    def setup_method(self):
        print("\n--- 方法前置：[setup_method] 重置应用状态或打开新页面 ---")
        
    def teardown_method(self):
        print("\n--- 方法后置：[teardown_method] 清除用例数据或截图 ---")

    def test_01(self):
        print("执行测试用例 01")

    def test_02(self):
        print("执行测试用例 02")

# 3. 模块级别：在当前整个 .py 脚本文件被加载和运行前后各执行一次（必须写在类外面）
def setup_module():
    print("\n--- 模块前置：[setup_module] 全局配置导入 ---")

def teardown_module():
    print("\n--- 模块后置：[teardown_module] 释放全局资源 ---")
```

---

### 2.2 现代 fixture + conftest 夹具系统

现代 pytest 推荐采用 `@pytest.fixture` 装饰器来实现更加灵活和精细的前后置。它通过 `yield` 分离前置与后置逻辑，并通过 `conftest.py` 实现多层级跨文件共享。

#### 2.2.1 核心机制与共享：`conftest.py`
* **conftest.py** 是 pytest 的专用局部配置文件，存放其中的 fixture 夹具会被同级及下级目录下的所有用例自动发现，无需手动导入。
* **前置与后置的分离**：在夹具函数中，`yield` 之前的代码作为**前置执行**，`yield` 之后的代码作为**后置清理**，同时 `yield` 还可以携带返回值，作为数据注入给测试用例。

#### 2.2.2 夹具作用域（Scope）参数深度解析
通过 `@pytest.fixture(scope="...", autouse=False)` 可以灵活调整夹具的生命周期。

| 作用域 (scope) | 执行频次与效果说明 | 典型应用场景 |
| :--- | :--- | :--- |
| **`function`** *(默认)* | **每个测试方法/函数执行前都会运行一次**。测试方法执行完毕后，执行 `yield` 之后的后置清理工作。各个测试用例之间完全独立，不共享夹具状态。 | 数据库单独事务重置、每个用例独立的数据清理、重新打开某个特定的APP页面。 |
| **`class`** | **每个测试类执行前运行一次**。即使类中有多个测试方法，该前置也只执行一次。在类中所有测试方法执行完毕后，运行 `yield` 后的后置清理。 | 实例化被测类、初始化页面对象（Page Object）、类级别的缓存或配置。 |
| **`module`** | **每个测试模块（即一个 `.py` 脚本文件）执行前运行一次**。在该模块内的所有测试类和方法全部执行完毕后，执行后置。 | 创建特定模块对应的数据库连接、启动高开销的局部系统服务、模块级全局 mock 数据初始化。 |
| **`package`** | **每个测试包（含有 `__init__.py` 的目录）执行前运行一次**。在该包下的所有子目录和测试文件运行完毕后执行后置。（需定义在包级目录下的 `conftest.py` 中）。 | 整个大型业务子系统级别的初始化，如特定子模块公用的长链接配置。 |
| **`session`** | **整个测试会话（即本次 `pytest` 运行的全部用例）开始前运行一次**。所有用例全部执行完毕后，执行后置。通常在根目录 `conftest.py` 中定义，可跨文件/目录全局共享。 | 自动化测试框架整体全局初始化、启动 APP/浏览器驱动、登录获取全局 Token/Session、创建全局数据库连接池。 |

#### 2.2.3 案例：手动调用与 `autouse` 自动执行
```python
# ==================== conftest.py ====================
import pytest

# 声明一个 session 级别的夹具，并携带返回值
@pytest.fixture(scope="session")
def enter_mine():
    print("\n[前置] Session 开始：启动 APP 并完成登录")
    yield "UserToken_XYZ123"  # 返回的数据会注入到引用该夹具的用例中
    print("\n[后置] Session 结束：关闭 APP，清理连接")

# 声明一个自动执行的 class 级别夹具
@pytest.fixture(scope="class", autouse=True)
def class_helper():
    print("\n[前置] Class 开始：准备当前测试类专属运行环境")
    yield
    print("\n[后置] Class 结束：清理当前测试类环境")
```

```python
# ==================== test_login.py ====================
import pytest

class TestLogin:
    # 只要在方法的形参中传入夹具名称，就能直接获取到 yield 传出的数据（依赖注入）
    def test_01_profile(self, enter_mine):
        print(f"执行 test_01_profile，使用的登录凭证为：{enter_mine}")
        assert enter_mine == "UserToken_XYZ123"

    def test_02_settings(self):
        print("执行 test_02_settings，此时 class_helper 依然有效")
```

---

## 3. pytest 高级功能与标记应用

### 3.1 mark 标记的核心应用

pytest 提供 `mark` 机制为测试用例打上额外的元数据标记，常用于：控制用例运行策略（如重跑、跳过）和自定义分类筛选（如冒烟测试）。

#### 3.1.1 失败用例重跑机制
在不稳定的网络环境或移动端测试中，为了排除偶然因素，可采用失败重跑策略。
* **安装插件**：`pip install pytest-rerunfailures`
* **使用标记**：`@pytest.mark.flaky(reruns=次, reruns_delay=秒)`

```python
import pytest

class TestLogin:
    # 如果测试失败，最多重跑 2 次，每次重跑之间间隔 1 秒
    @pytest.mark.flaky(reruns=2, reruns_delay=1)
    def test_login_success(self):
        print("执行登录用例")
        # 模拟偶然失败
        assert 1 == 2
```

#### 3.1.2 跳过用例执行
* **无条件跳过**：`@pytest.mark.skip(reason="...")`
* **有条件跳过**：`@pytest.mark.skipif(condition, reason="...")`

```python
import pytest

class TestAppUpdate:
    CURRENT_VERSION = 1.0

    # 当版本是 1.0 时跳过该测试
    @pytest.mark.skipif(CURRENT_VERSION == 1.0, reason="1.0版本暂未开放该功能，跳过测试")
    def test_high_level_feature(self):
        print("执行高阶功能测试")

    # 无条件跳过
    @pytest.mark.skip(reason="该用例对应的业务逻辑已作废，直接跳过")
    def test_obsolete_feature(self):
        pass
```

#### 3.1.3 自定义标记与用例筛选
在项目庞大时，我们常需要针对特定场景筛选用例（如只运行冒烟测试用例）。
1. **在 `pytest.ini` 中声明标记，防止警告**：
   ```ini
   [pytest]
   markers =
       smoke: 冒烟测试
   ```
2. **在测试方法上应用装饰器**：
   ```python
   import pytest

   class TestOrder:
       @pytest.mark.smoke
       def test_order_success(self):
           print("执行下单（冒烟测试用例）")
           assert True
   ```
3. **在命令行筛选运行**：
   ```bash
   # 只执行被标记为 smoke 的测试用例
   pytest -m smoke
   
   # 执行非 smoke 标记的测试用例
   pytest -m "not smoke"
   ```

---

### 3.2 装饰器装配与运行执行顺序 (洋葱模型)

在 Python 中，当测试方法上同时存在多个装饰器（如 `@pytest.mark.smoke`、`@pytest.mark.flaky`、`@pytest.mark.parametrize` 等）时，我们需要清晰认识它们的**装配顺序**与**执行逻辑**。

#### 3.2.1 经典洋葱模型 (Onion Model)
* **装配阶段（定义时/编译时）**：离方法定义**越近的装饰器，越先装配**（自底向上）。
* **执行阶段（运行时）**：离方法定义**越远的装饰器，其前置逻辑越先运行**（自顶向下，类似于洋葱皮，外层先被拨开，最底层最晚触及）。

##### 执行顺序原理示意图：
```text
      ┌────────────────────────────────────────────────────────┐
      │ 【最外层】 外部装饰器 (Decorator Outer)                  │
      │   ┌──────────────────────────────────────────────────┐ │
      │   │ 【最内层】 内部装饰器 (Decorator Inner)            │ │
      │   │   ┌────────────────────────────────────────────┐ │ │
      │   │   │     ★★★ 目标测试方法 (Test Method) ★★★   │ │ │
      │   │   └────────────────────────────────────────────┘ │ │
      │   └──────────────────────────────────────────────────┘ │
      └────────────────────────────────────────────────────────┘
       ▲                                                    │
       └───── [前置步骤：从外到内] ────── [后置步骤：从内到外] ──────┘
```

#### 3.2.2 运行代码实证

```python
import pytest

# 自定义装饰器展示装配与执行顺序
def decorator_outer(func):
    print(">>> [装配阶段] 正在加载 外部 装饰器 (decorator_outer) <<<")
    def wrapper(*args, **kwargs):
        print("[运行阶段] 执行 外部 装饰器 的前置逻辑")
        res = func(*args, **kwargs)
        print("[运行阶段] 执行 外部 装饰器 的后置逻辑")
        return res
    return wrapper

def decorator_inner(func):
    print(">>> [装配阶段] 正在加载 内部 装饰器 (decorator_inner) <<<")
    def wrapper(*args, **kwargs):
        print("[运行阶段] 执行 内部 装饰器 的前置逻辑")
        res = func(*args, **kwargs)
        print("[运行阶段] 执行 内部 装饰器 的后置逻辑")
        return res
    return wrapper

class TestDecoratorOrder:
    
    @decorator_outer  # 离方法较远（后装配，但在运行时最外层，前置最先执行）
    @decorator_inner  # 离方法最近（先装配，但在运行时最内层，直接包裹方法）
    def test_demo(self):
        print("    ★ 执行测试方法 test_demo 本身 ★")
```

##### 理论控制台输出结果：
```text
>>> [装配阶段] 正在加载 内部 装饰器 (decorator_inner) <<<
>>> [装配阶段] 正在加载 外部 装饰器 (decorator_outer) <<<

[运行阶段] 执行 外部 装饰器 的前置逻辑
[运行阶段] 执行 内部 装饰器 的前置逻辑
    ★ 执行测试方法 test_demo 本身 ★
[运行阶段] 执行 内部 装饰器 的后置逻辑
[运行阶段] 执行 外部 装饰器 的后置逻辑
```

#### 3.2.3 核心结论
1. **定义离方法越近，先装配**：`decorator_inner` 紧挨着方法定义，它最先获取到测试方法的函数引用进行第一层包裹。
2. **运行离方法越远，先执行前置**：由于 outer 包裹在 inner 之外，当 pytest 触发方法时，外部 outer 装饰器最先接收到调用，故 outer 的前置先执行。

#### 3.2.4 扩展：堆叠参数化装饰器 `@pytest.mark.parametrize` 时的执行顺序
若测试用例堆叠了多个参数化装饰器：
```python
@pytest.mark.parametrize("x", [1, 2])
@pytest.mark.parametrize("y", ["A", "B"])
def test_cartesian(self, x, y):
    print(f"执行用例組合: {x}, {y}")
```
* 按照洋葱模型，底部的参数 `y` 是内层包裹，顶部的参数 `x` 是外层包裹。
* pytest 在执行参数组合时，底部的参数 `y` 会变成**内层循环**（变化频率最快），顶部的 `x` 变成**外层循环**。
* 最终生成和运行测试的顺序为：
  1. `x=1, y="A"`
  2. `x=1, y="B"`
  3. `x=2, y="A"`
  4. `x=2, y="B"`

---

## 4. 数据驱动测试 (DDT)

数据驱动测试（Data-Driven Testing, DDT）是把测试数据与代码逻辑相分离的一种自动化测试架构设计。通过大批量、覆盖不同边界和异常场景的数据文件驱动相同的用例逻辑反复运行。

### 4.1 JSON 数据读取

在 `tools/read_json.py` 文件中，我们通常编写一个读取 JSON 数据文件的通用方法：

```python
import json

def read_json(file_path):
    """
    通用读取 JSON 数据方法
    :param file_path: 数据文件路径
    :return: 包含元组的列表，例如 [("username_1", "pwd_1", "toast_1"), ...]
    """
    with open(file_path, "r", encoding="utf-8") as f:
        data = json.load(f)
    
    # 将列表嵌套的字典格式转为列表嵌套元组，便于 pytest.mark.parametrize 消费
    result = []
    for item in data:
        # 获取字典所有的 value 组成元组
        result.append(tuple(item.values()))
    return result
```

#### JSON 数据文件案例 (`data/order_data.json`)：
```json
[
  {
    "desc": "下单成功",
    "order_id": "ORD20269999",
    "expect": "确认订单成功"
  },
  {
    "desc": "库存不足",
    "order_id": "ORD20268888",
    "expect": "库存不足，下单失败"
  }
]
```

---

### 4.2 参数化用例实现

通过 `@pytest.mark.parametrize` 装饰器将读取到的测试数据注入到用例中：

```python
import pytest
from tools.read_json import read_json

class TestOrder:

    # 1. 声明接收变量名，多个变量之间用逗号拼接
    arg_names = "desc, order_id, expect"

    # 2. parametrize 第一个参数是逗号隔开的变量名字符串，第二个参数是包含元组的列表数据
    @pytest.mark.parametrize(arg_names, read_json("./data/order_data.json"))
    def test_order_settlement(self, desc, order_id, expect):
        """
        测试订单结算流程
        """
        print(f"\n当前执行用例场景: {desc}")
        print(f"输入测试数据 order_id: {order_id}")
        
        # 模拟模拟被测方法调用
        actual_result = "确认订单成功" if order_id == "ORD20269999" else "库存不足，下单失败"
        
        # 断言结果
        assert actual_result == expect
```

---

## 5. Faker 随机测试数据库

在日常的自动化测试中，为了解决账号、用户名、身份证等唯一性校验限制，我们需要动态、随机地生成一些逼真的模拟数据。

* **安装 Faker 库**：`pip install faker`

```python
from faker import Faker

# 初始化 Faker 实例，指定 locale="zh_CN" 可以输出地道的中文测试数据
fk = Faker(locale="zh_CN")

# 1. 动态生成符合规范的随机中国公民身份证 (ssn)
CARD = fk.ssn()

# 2. 动态生成符合规范的随机中国大陆手机号码 (phone_number)
PHONE = fk.phone_number()

# 3. 动态生成逼真的随机中文人名 (name)
NAME = fk.name()

# 4. 动态生成其他常用模拟数据
EMAIL = fk.email()            # 随机电子邮箱
ADDRESS = fk.address()        # 随机中文地址
JOB = fk.job()                # 随机职业
COMPANY = fk.company()        # 随机公司名

print(f"生成的虚拟姓名: {NAME}")
print(f"生成的虚拟手机: {PHONE}")
print(f"生成的虚拟身份证: {CARD}")
print(f"生成的虚拟邮箱: {EMAIL}")
print(f"生成的虚拟地址: {ADDRESS}")
```

---

## 6. Allure 专业测试报告集成

Allure 是一款功能极为强大、外观现代且支持丰富元数据标记的测试报告系统。

### 6.1 环境搭建与 ini 配置

#### 1. 插件安装
```bash
# 安装 pytest 运行支持组件
pip install allure-pytest
```

#### 2. 在 `pytest.ini` 中添加配置项
在运行 pytest 时，为了使 Allure能正确捕获和记录测试数据，必须添加 `--alluredir` 参数。

```ini
[pytest]
addopts = -s --alluredir ./report --clean-alluredir
```
*(注：`--clean-alluredir` 用于保证每次运行前清除该目录下的历史残留临时 JSON/txt 文件)*

---

### 6.2 在线报告与离线 HTML 报告生成

当 pytest 执行完毕后，会在 `./report` 目录下生成一系列原始的 JSON 格式测试数据，无法直接双击查看。我们需要将其转换并渲染成网页格式。

#### 1. 生成在线临时报告（热服务方式）
此方式不需要磁盘落地，生成完会自动开启端口并在浏览器展示：
```bash
# 在项目根路径下终端运行
allure serve ./report
```

#### 2. 生成离线静态 HTML 测试报告
为了便于在 Jenkins 等 CI/CD 中拉取归档、邮件传输或分发给非测试人员查看，我们需要将其渲染成一个纯静态的 HTML 文件夹：

在项目根目录下，新建一个 `cmd_allure.py` 文件，用于快速封装渲染生成命令：

```python
# ==================== cmd_allure.py ====================
import os

# 1. 定义 Allure 命令
#    generate : 生成测试报告指令
#    ./report : 运行 pytest 后产生的临时 json 原始数据路径
#    -o ./new_report : 输出渲染后的纯 HTML 静态文件夹路径为 ./new_report
#    --clean : 在生成新报告之前清空已存在的旧 HTML 文件夹
run_cmd = "allure generate ./report -o ./new_report --clean"

print("正在调用本地系统 Allure 引擎，准备生成离线 HTML 测试报告...")
# 2. 通过系统命令行执行打包
os.system(run_cmd)
print("离线 HTML 测试报告生成完毕！可前往 ./new_report/index.html 直接在浏览器打开查看。")
```

#### 3. 完整的工作流执行流程
在日常测试流程中，只需在命令行终端输入如下两个简单命令即可完成“执行 -> 生成报告”全套动作：
```bash
# 第一步：运行自动化测试用例，生成原始 report 数据
pytest

# 第二步：执行打包脚本，生成离线 HTML 报告
python cmd_allure.py
```
完成后，打开 `./new_report/index.html`，即可欣赏酷炫且专业的测试报告！
