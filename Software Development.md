# Python软件开发（Flet）
## 目录
- [1. 安装Flet环境](#安装Flet环境)
- [2. 编辑Flet框架](#编辑Flet框架)
- [3. 基本功能](#基本功能)
    - [3.1 创建基本窗口](#创建基本窗口)
    - [3.2 多行输入框](#多行输入框)

<a name="安装Flet环境"></a>
#### 1. 安装Flet环境

下载`flet`环境：
```python
pip install flet
```
下载`desktop`桌面支持：
```python
pip install flet-desktop
```

<a name="编辑Flet框架"></a>
#### 2. 编辑Flet框架

```python
import flet as ft  # 导入flet

def main(page: ft.Page):  # flet程序主执行体
    ...  # 程序内容在这里
    page.update()  # 刷新页面，必须存在，表示应用main

ft.app(target=main)  # 启动flet应用
```

<a name="基本功能"></a>
#### 3. 基本功能

<a name="创建基本窗口"></a>
##### 3.1 创建基本窗口

```python
def main(page: ft.Page):
    initialize_window(page)  # 在main中导入窗口设置

def initialize_window(page: ft.Page):  # 初始化窗口的函数
    page.title = "窗口标题"
    page.window_width = 600  # 窗口宽度
    page.window_height = 800  # 窗口高度
    # page.window_resizable = False  # 禁止调整窗口大小
```

<a name="多行输入框"></a>
##### 3.2 多行输入框

```python
def main(page: ft.Page):
    text_input(page)  # 导入输入框

def text_input(page: ft.Page):  # 输入框组件
    # 创建文本输入框
    global text_input
    text_input = ft.TextField(
        width = page.window_width * 0.5,  # 输入框宽度（设置为窗口的一半）
        text_align = ft.TextAlign.LEFT,  # 输入框文本左对齐
        border_color = "white",  # 设置边框颜色
        multiline = True  # 多行输入支持
    )
    # 创建发送按钮
    send_button = ft.IconButon(
        icon = ft.Icons.ARROW_UPWARD,  # 使用内置图标
        on_click = lambda e: (  # 定义点击事件
            print("发送消息: ", text_input.value),  # 在控制台打印发送的文本信息
            setattr(text_input, 'value', ''),  # 清空输入框的内容
            page.update()  # 刷新界面
        )
    )
    # 设置键盘发送、换行事件
    def handle_key_down(e):
        if e.key == "Enter" and not e.shift:  # 捕捉键盘事件，如果只按下回车
            print("发送消息: ", text_input.value)  # 在控制台打印发送的内容
            text_input.value = ""  # 清空输入框
            page.update()  # 刷新页面
        else e.shift and e.key == "Enter":  # 捕捉键盘事件，如果按下了Shift和Enter
            text_input.value += "\n"  # 输入框添加换行
            page.update()  # 刷新页面
```