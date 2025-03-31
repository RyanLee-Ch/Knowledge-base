<h1 style="text-align: center;">React</h1>

- [一、项目创建](#项目创建)
- [二、组件](#组件)
    - [1 组件的定义](#组件的定义)
    - [2 创建组件](#创建组件)
        - [2.1 组件目录创建](#组件目录创建)
        - [2.2 创建组件.jsx](#创建组件.jsx)
        - [2.3 创建组件样式.module.scss](#创建组件样式.module.scss)

---

<a name="项目创建"></a>

### 一、创建项目
#### 1.使用Vite创建React项目：
```cmd
npm create vite@latest 项目名 -- --template react
cd 项目名
npm install
npm install sass --save-dev  // 创建scss样式支持
```

---

<a name="组件"></a>

### 二、组件

<a name="组件的定义"></a>

#### 1.组件的定义
组件是可重复使用的代码块，有自己的样式、功能、页面，且能够独立存在。在出现以下的情况，可以使用组件：
- 重复代码
- 超过50行的代码
- 需要单独测试的模块
- 需要协作开发

根据应用场景的不同，一般为以下结构（示例）：
```
src/
├── components/          # 通用组件（全站复用）
│   ├── Layout/          # 全局布局组件
│   │   ├── Header.jsx
│   │   ├── Header.module.scss
│   │   ├── Footer.jsx
│   │   ├── Footer.module.scss
│   │   ├── Sidebar.jsx
│   │   └── Sidebar.module.scss
│   ├── UI/              # 基础UI组件
│   │   ├── Button.jsx
│   │   └── Modal.jsx
│   └── Features/        # 业务功能组件
│       ├── SearchBar.jsx
│       ├── SearchBar.module.scss
│       ├── CartWidget.jsx
│       └── CartWidget.module.scss
│
├── pages/               # 页面级组件（按路由划分）
│   ├── Home/
│   │   ├── HeroSection.jsx
│   │   ├── HeroSection.module.scss
│   │   ├── ProductGrid.jsx
│   │   └── ProductGrid.module.scss
│   ├── Product/
│   │   ├── ProductDetail.jsx
│   │   ├── ProductDetail.module.scss
│   │   ├── ReviewsSection.jsx
│   │   └── ReviewsSection.module.scss
│   └── Checkout/
│       ├── PaymentForm.jsx
│       ├── PaymentForm.module.scss
│       ├── OrderSummary.jsx
│       └── OrderSummary.module.scss
│
├── routes/              # 路由配置
│   └── index.js
│
└── App.jsx              # 根组件
```

<a name="创建组件"></a>

#### 2.创建组件

<a name="组件目录创建"></a>

##### 2.1 组件目录创建：
在`/src`中创建目录`/components`（建议根据推荐结构继续细分），该目录用于存放**组件`.jsx`**、**样式`.scss`** 文件。

<a name="创建组件.jsx"></a>

##### 2.2 创建组件.jsx：
举例创建Button组件`Button.jsx`：
```js
import styles from './Button.module.scss';

export default function Button({ children }) {
  return (
    <button className={styles.button}>
      {children}
    </button>
  );
}
```
解释：
- 导入同目录下，名为`Button.module.scss`的scss样式：
```js
import styles from './Button.module.scss';
```
- 创建一个开放的函数组件：
```js
// export default function：声明开放函数
// Button：命名为Button
// children：组件通信（接收标签内容）
export default function Button({children}){
    ...
}
```
- 渲染JSX：
```js
// return (...)：渲染JSX内容
// className：React调用class的一种方式
// styles.button：调用Button.module.scss中的button样式
// {children}：渲染children中的内容
  return (
    <button className={styles.button}>
      {children}
    </button>
  );
```

<a name="创建组件样式.module.scss"></a>

##### 2.3 创建组件样式.module.scss
举例创建`Button.jsx`的组件样式`Button.module.scss`：
```css
.button {  // 通过className={styels.button}调用
  padding: 12px 24px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  transition: background-color 0.3s;

  // SCSS 嵌套语法
  &:hover {  // 自动生效，不需要className调用
    background-color: darken(#4CAF50, 10%);
  }

  // 支持动态类名
  &--secondary {  // 通过className={styles['button==secondary']}调用
    background-color: #008CBA;
  }
}
```
解释：
- 定义CSS选择器
```css
// 使用 . 符号定义名为button的类选择器
.button {
  ...
}
```

<a name="创建全局组件样式：globals.scss"></a>

##### 2.4 创建全局组件样式：globals.scss
创建：`src/styels/globals.scss`，定义如下：
```scss
:root {  // 定义全局变量
  --primary-color: #4CAF50;
}

body {  // 全局基础样式
  margin: 0;
  font-family: system-ui;
}

//其它均可自定
```

##### 2.5 引入全局样式：
通过在`/src/main/jsx`中引入：
```jsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import './styles/globals.scss'; // 添加这一行

ReactDOM.createRoot(document.getElementById('root')).render(
  ...
);
```

##### 2.6 CSS样式列表：
CSS选择器分有很多类，有：标签选择器、类选择器、ID选择器、通配符选择器 等；

1. 标签选择器：`div { color: red; }`：将所有div标签的color设置为red；
2. 类选择器：`.button { padding: 10px; }`：设定一个名为button的类选择器，能够被`className={styles.button}`标记的**多个标签**调用
3. ID选择器：`#header { height: 60px; }`：设定一个名为header的ID选择器，能够被`id={header}`标记的

###### 布局类CSS：
|属性|作用|属性值|示例|
|:-:|:-:|:-:|:-:|
|`display`|元素显示模式|`flex`, `grid`，`block`|`display: flex;`|
|`position`|定位方式|`relative`，`absolute`|`position: relative;`|
|`top/left`|定位偏移|`px`，`%`|`top: 100px;`|
|`flex-direction`|Flex容器排列方向|`row`，`column`|`flex-direction: row;`|
|`justify-content`|主轴对齐方式|`center`，`space-between`|`justify-content: center;`|
|`align-items`|交叉轴对齐方式|`stretch`，`flex-start`|`align-items: stretch;`|

###### 盒模型CSS：
|属性|作用|属性值|示例|
|:-:|:-:|:-:|:-:|
|`width`|宽度|`px`，`%`|`width: 200px;`|
|`padding`|内边距|`px`，`%`|`padding: 20px;`|
|`margin`|外边距|`auto`，`px`，`%`|`margin: 10px auto`|
|`border`|边框|`px solid/dashed color`|`border: 2px dashed red;`|

###### 文本样式CSS：
|属性|作用|属性值|示例|
|:-:|:-:|:-:|:-:|
|`color`|文本颜色|`#十六进制色号`，`rgba(RGBA代码)`，`颜色单词`|`color: red;`|
|`font-size`|字体大小|`px`，`rem`|`font-size: 2rem;`|
|`font-weight`|字体粗细|`bold`，`具体大小`|`font-weight: bold;`|
|`text-align`|水平对齐|`left`，`center`|`text-align: center;`|
|`line-height`|行高|`px`，`具体值`|`line-height: 1.5;`|
|`text-decoration`|文本装饰|`underline`，`none`|`text-decoration: underline;`|

###### 背景与边框CSS：
|属性|作用|属性值|示例|
|:-:|:-:|:-:|:-:|
|`background-color`|背景颜色|`transparent`，`#十六进制色号`，`颜色单词`|`background-color: #f0f0f0;`|
|`background-image`|北京图片|`url('图片路径')`|`background-image: url('image.jpg');`|
|`border-radius`|圆角|`px`，`%`|`border-radius: 50%;`|
|`box-shadow`|阴影|`2px 2px 10px rgba(0,0,0,0.1)`|`box-shadow: 2px 2px 10px rgba(0,0,0,0.1);`|

###### 动画与过渡CSS：
|属性|作用|属性值|示例|
|:-:|:-:|:-:|:-:|
|`transition`|过渡效果|`all 0.3s ease-in-out`|`transition: transform 0.3s;`|
|`animation`|关键帧动画|`slide 1s infinite`|/|
|`transform`|变形效果|`rotate(45deg)`，`scale(1.2)`|/|

#### 3.注册组件

##### 3.1 组件预处理
清空组件内容，写入新结构
```jsx
function App() {  // 函数体
  return (  // 渲染体，其中<div>为根标签，可以设为幽灵标签
    <div>
    </div>
  );
}

export default App;
```
##### 3.2 新编写组件：
将示例的`Button.jsx`组件带入：
```jsx
import Button from './components/Button/Button.jsx';

function App() {
  return (
    <div>
      <Button>Primary Button</Button>
      <Button>Secondary Button</Button>
    </div>
  );
}

export default App;
```
解释：
- 从`/components`组件库中导入组件：
```jsx
// 导入组件格式：import 组件名 from '组件路径'
import Button from './components/Button/Button.jsx'
```
- 将组件放入`App.jsx`渲染：
```jsx
return (  // return结构体中均是被渲染对象
  <div>
    <Button>带内容渲染</Button>
    <Button />  
  </div>
);
```

#### 4.项目运行
##### 4.1 本地运行测试
通过在命令行`cd /项目目录`进入项目根目录，启动项目的本地运行：
```cmd
npm run dev
```
