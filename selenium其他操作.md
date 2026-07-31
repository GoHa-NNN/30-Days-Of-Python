自动化测试中，除了元素定位和点击、输入之外，控制浏览器本身以及处理弹窗、页面滚动、多标签页切换等功能非常常见。这些通常被称为**浏览器级操作**或**控制级操作**。

我为你整理了 Selenium 中控制浏览器窗口最大化，以及其他最常用的核心非定位操作。

## 1. 窗口控制（最大化、全屏、缩放）

控制浏览器窗口的大小通常在启动浏览器后第一时间执行。

Python

```
from selenium import webdriver

driver = webdriver.Chrome()

# 1. 窗口最大化（最常用）
driver.maximize_window()

# 2. 全屏（类似按了 F11，没有浏览器边框和地址栏）
driver.fullscreen_window()

# 3. 设置固定的窗口大小（宽, 高）- 常用于模拟手机或平板尺寸
driver.set_window_size(1920, 1080)

# 4. 获取当前窗口的大小和坐标
size = driver.get_window_size()
position = driver.get_window_position()
```

## 2. 页面导航操作

控制浏览器的前进、后退和刷新。

Python

```
# 打开一个网页（你肯定已经知道了）
driver.get("https://www.example.com")

# 1. 刷新当前页面（等同于按 F5）
driver.refresh()

# 2. 浏览器后退（点击左上角回退箭头）
driver.back()

# 3. 浏览器前进（点击左上角前进箭头）
driver.forward()
```

## 3. 多标签页（窗口）切换

当点击某个链接弹出了一个新的浏览器标签页时，Selenium 并不会自动把控制权移过去，你需要手动切换“句柄（Handle）”。

Python

```
# 1. 获取当前窗口的句柄
current_handle = driver.current_window_handle

# 执行了某个点击，触发了新标签页打开...

# 2. 获取当前浏览器“所有”打开的窗口句柄（返回一个列表,列表从0开始按操作时序记录）
all_handles = driver.window_handles

# 3. 切换到最新的那个标签页（列表里的最后一个）
driver.switch_to.window(all_handles[-1])

# 4. 关闭当前标签页（注意：close只会关掉当前页，quit会关闭整个浏览器程序）
driver.close()

# 5. 切回原本的第一个网页
driver.switch_to.window(all_handles[0])
```

## 4. 页面滚动（Scroll）

Selenium 本身没有直接提供 scroll 的方法，我们通常需要借助执行 JavaScript 代码来实现滚动。

Python

```
# 1. 向下滚动固定高度（例如向下滚动 500 像素）
driver.execute_script("window.scrollBy(0, 500);")

# 2. 滚动到页面最底部
driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")

# 3. 滚动到某个特定元素可见的位置（假设 target_element 是你已经定位到的元素）
driver.execute_script("arguments[0].scrollIntoView();", target_element)
```

## 5. 处理 Iframe（内嵌网页）

有些网页里面嵌套了另一个网页（）。如果目标元素在 iframe 里面，直接定位会报错，必须先“跳进去”。

Python

```
# 1. 切换进入 iframe（可以通过 iframe 的 id、name，或者先定位到 iframe 元素再传进来）
driver.switch_to.frame("iframe_id_or_name")

# 在 iframe 内部进行元素定位和操作...

# 2. 操作完后，必须切回到最外层的骨架页面，否则无法操作外面的元素
driver.switch_to.default_content()
```

## 6. 处理浏览器原生弹窗（Alert）

当网页弹出 JavaScript 的 alert、confirm 或 prompt 提示框时，普通的 HTML 定位是无效的。

Python

```
# 1. 切换到弹窗上
alert = driver.switch_to.alert

# 2. 获取弹窗里的文本内容
print(alert.text)

# 3. 点击弹窗的“确定”
alert.accept()

# 4. 点击弹窗的“取消”（如果有的话）
# alert.dismiss()

# 5. 如果是 prompt 弹窗，可以在里面输入文字
# alert.send_keys("输入的内容")
```

## 7. 获取页面基本信息（断言常用）

用于验证你是否成功跳转到了正确的页面。

Python

```
# 1. 获取当前页面的 Title（标签页标题）
page_title = driver.title

# 2. 获取当前页面的完整 URL 地址
current_url = driver.current_url

# 3. 获取当前页面的 HTML 源代码（常用于排查定位不到的元素或配合 BeautifulSoup 解析）
page_source = driver.page_source
```

## 8. 屏幕截图

代码跑自动化时，报错时自动截个图是非常好的习惯。

Python

```
# 1. 截取当前整个浏览器屏幕，保存为图片文件
driver.save_screenshot("error_report.png")

# 2. 也可以只截取某一个特定元素的图
# target_element.screenshot("element_only.png")
```