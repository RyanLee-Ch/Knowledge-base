<h1 style="text-align: center;">Markdown语法</h1>

## 目录
- [目录设置](#目录设置)
- [标题](#标题)
- [字符](#字符)
- [表格](#表格)
  - [基础表格](#基础表格)
  - [复杂表格](#复杂表格)
- [代码块](#代码块)
- [列表](#列表)
  - [有序列表](#有序列表)
  - [无序列表](#无序列表)
  - [任务列表](#任务列表)
- [数学公式](#数学公式)
- [插入媒体文件](#插入媒体文件)
  - [插入图片](#插入图片)
  - [插入视频](#插入视频)
- [修饰内容](#修饰内容)
  - [打断横线](#打断横线)
  - [引用补充](#引用补充)
  - [文字居中](#文字居中)


<a name="目录设置"></a>
## 目录设置
```markdown
- [目录标题](#超链接名)
...
...
<a name="超链接名"></a>
##目录标题
```

<a name="标题"></a>

## 标题
|标识符号|意义|示例|
|:---:|:-----:|:----:|
|`#`|一级标题|`#主题`|
|`##`|二级标题|`##子主题`|
|···|||
|`######`|六级标题|`######最底层标题`|
---

<a name="字符"></a>

## 字符设置
|标识符号|意义|示例效果|
|:---:|:---:|:-----:|
|\*text*|斜体|*你好*|
|\*\*text**|加粗|**你好**|
|\`text`|行内代码|`print("你好")`|
|\<u>text\</u>|下划线|<u>你好</u>|
|\:text|emoji表情|:s|
|\$text$|行内公式（后面会讲）|$\theta=x^2$|
|\~text~|下标|H~2~O|
|\^text^|上标|X^2^|
|\==text==|高亮|==你好==|
|\[text](URL)|超链接|[百度](www.baidu.com)|
---

<a name="表格"></a>

## 表格
<a name="基础表格"></a>
#### Markdown基本表格
|标题A|标题B|标题C|
|:---|:---:|----:|
|内容A|内容B|内容C|
...
|内容X|内容Y|内容Z|
```python
|标题A|标题B|标题C|  # 标题栏
|:---|:---:|----:|  # 位置属性设置，依次对应：居左、居中、居右
|内容A|内容B|内容C|
...
|内容X|内容Y|内容Z|
```
<a name="复杂表格"></a>
#### HTML复杂表格
<table>
  <tr>
    <th>标题A</th>
    <th>标题B</th>
  </tr>
  <tr>
    <td>内容A</td>
    <td>内容B</td>
  </tr>
  <tr>
    <td colspan="2">合并单元格显示</td>
  </tr>
  <tr>
    <td>内容X</td>
    <td>内容Z</td>
  </tr>
</table>

```html
<table>
  <tr>
    <th>标题A</th>
    <th>标题B</th>
  </tr>
  <tr>
    <td>内容A</td>
    <td>内容B</td>
  </tr>
  <tr>
    <td colspan="2">合并单元格显示</td>
  </tr>
  <tr>
    <td>内容X</td>
    <td>内容Z</td>
  </tr>
</table>
```
---

<a name="代码块"></a>

## 代码块
```python
这是示例：print("Hello World")
```
实现方式：
```markdown
前导标识：```python

结尾标识：```
```
---

<a name="列表"></a>
## 列表
<a name="有序列表"></a>
#### 有序列表
1. 开门
1.1 解锁
1.2 按下门把手 
2. 关门
3. 吃饭睡觉
```markdown
1. 开门
1.1 解锁
1.2 按下门把手 
2. 关门
3. 吃饭睡觉
```
<a name="无序列表"></A>
#### 无序列表
- 开门
  - 解锁
  - 按下门把手
- 关门
- 吃饭睡觉
```markdown
- 开门
  - 解锁
  - 按下门把手
- 关门
- 吃饭睡觉
```
<a name="任务列表"></a>
#### 任务列表
- [ ] 吃饭
- [ ] 喝水
- [x] 睡觉
```markdown
- [ ] 吃饭
- [ ] 喝水
- [x] 睡觉
```
---
<a name="数学公式"></a>
## 数学公式
$$
\frac{\partial f}{\partial x} = 2 \sqrt{a}x
$$
```markdown
$$
\frac{\partial f}{\partial x} = 2 \sqrt{a}x
$$
```
---

<a name="插入媒体文件"></a>
## 插入媒体文件
<a name="插入图片"></a>
#### 插入图片
![百度](https://www.baidu.com/img/flexible/logo/pc/result.png)
```python
![百度](https://www.baidu.com/img/flexible/logo/pc/result.png)
```
---
<a name="插入视频"></a>
#### 插入视频
使用ifram标签，一般视频网站自带（直接复制）：
```html
<iframe src="//player.bilibili.com/player.html?isOutside=true&aid=327623069&bvid=BV1JA411h7Gw&cid=171385214&p=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>
```

<a name="修饰内容"></a>
## 修饰内容
<a name="打断横线"></a>
#### 打断横线
每部分都有的
```markdown
---
```
<a name="引用补充"></a>
#### 引用/补充
你好
> 这是补充
---
<a name="文字居中"></a>
#### 文字居中
<p style="text-align: center;">你好</p>

```html
<p style="text-align: center;">你好</p>
```