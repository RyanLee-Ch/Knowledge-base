<h1 style="text-align: center;">React</h1>

- [一、项目创建](#项目创建)
  - [1.1 使用Vite创建React项目](#使用Vite创建React项目)
- [二、组件](#组件)
    - [2.1 组件的定义](#组件的定义)
    - [2.2 创建组件](#创建组件)
        - [2.2.1 组件目录创建](#组件目录创建)
        - [2.2.2 创建组件.jsx](#创建组件.jsx)
        - [2.2.3 创建组件样式.module.scss](#创建组件样式.module.scss)
        - [2.2.4 创建全局组件样式：globals.scss](#创建全局组件样式：globals.scss)
        - [2.2.5 引入全局样式：globals.scss](#引入全局样式：globals.scss)
        - [2.2.6 调用全局变量](#调用全局变量)
        - [2.2.7 CSS样式列表](#CSS样式列表)
    - [2.3 注册组件](#注册组件)
      - [2.3.1 组件预处理](#组件预处理)
      - [2.3.2 新编写组件](#新编写组件)
    - [2.4 组件通信](#组件通信)
      - [2.4.1 Props传递](#Props传递)
      - [2.4.2 createContext跨组件通信](#createContext跨组件通信)
    - [2.5 条件渲染](#条件渲染)
      - [2.5.1 条件判断渲染](#条件判断渲染)
      - [2.5.2 三元判断渲染](#三元判断渲染)
      - [2.5.3 短路与判断渲染](#短路与判断渲染)
    - [2.6 列表渲染](#列表渲染)
    - [2.7 钩子函数](#钩子函数)
      - [2.7.1 useState状态管理](#useState状态管理)
      - [2.7.2 useEffect副作用](#useEffect副作用)
        - [全量监控模式](#全量监控模式)
        - [单次执行模式](#单次执行模式)
        - [精准监控模式](#精准监控模式)
        - [定时触发模式](#定时触发模式)
- [三、组件进阶](#组件进阶)
  - [3.1 组件组合](#组件组合)
  - [3.2 HOC高阶组件](#HOC高阶组件)
- [四、路由配置](#路由配置)
- [、项目运行](#项目运行)
  - [3.1 本地运行React](#本地运行React)

---

<a name="项目创建"></a>
### 一、创建项目
<a name="使用Vite创建React项目"></a>
#### 1.1 使用Vite创建React项目：
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
#### 2.1 组件的定义
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
#### 2.2 创建组件

<a name="组件目录创建"></a>
##### 2.2.1 组件目录创建：
在`/src`中创建目录`/components`（建议根据推荐结构继续细分），该目录用于存放**组件`.jsx`**、**样式`.scss`** 文件。

<a name="创建组件.jsx"></a>
##### 2.2.2 创建组件.jsx：
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
##### 2.2.3 创建组件样式.module.scss
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
##### 2.2.4 创建全局组件样式：globals.scss
创建：`src/styels/globals.scss`，定义如下：
```scss
:root {  // 定义全局变量
  --primary-color: #4CAF50;  // --primary-color为变量名；
}

body {  // 全局基础样式
  margin: 0;
  font-family: system-ui;
}

//其它均可自定
```

<a name="引入全局样式：globals.scss"></a>
##### 2.2.5 引入全局样式：globals.scss：

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
<a name="调用全局变量"></a>
##### 2.2.6 调用全局变量：
当全局样式已经在`main.jsx`中被导入后，可以在其他scss中通过`var()`调用全局变量
```scss
// Button.scss:
.button {
  background-color: var(--primary-color);  // 调用全局变量
}
```

<a name="CSS样式列表"></a>
##### 2.2.7 CSS样式列表：
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

<a name="注册组件"></a>
#### 2.3 注册组件

<a name="组件预处理"></a>
##### 2.3.1 组件预处理

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

<a name="新编写组件"></a>
##### 2.3.2 新编写组件：

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

<a name="组件通信"></a>
#### 2.4 组件通信

<a name="Props传递"></a>
##### 2.4.1 Props传递

在创建组件`.jsx`时，对组件创建`{ Props }`对象，如下：
```jsx
export default function UserCard({ name, age}) {
  ...
}
```
将Props对象渲染至HTML中：
```jsx
return (
  <div className={ sytles.card }>
    <h3>{name}<h3/>  {/* 使用 "{} + Props对象" 实现渲染 */}
    <p>{age}</p>  {/* 同上 */}
  </div>
);
```

<a name="createContext跨组件通信"></a>
##### 2.4.2 createContext跨组件通信

通过创建`Context`共享数据组件、`Provider`数据提供组件、`useContext`数据源组件，实现数据公开，可以让各个组件无视多层传递prop：
###### 创建共享数据组件
```jsx
import { createContext } from ' react';  // 导入createContext

const UserContext = createContext();  // 创建空箱子
export default UserContext; 
```
###### 创建数据提供组件

<a name="条件渲染"></a>
#### 2.5 条件渲染

（判断当某个条件达成时，才会渲染JSX）

<a name="条件判断渲染"></a>
##### 2.5.1 条件判断渲染（单独创建`function`，使用`if-else`语句）：

```jsx
function Greeting({ isLoggedIn }){  {/* isLoggedIn是一个用于判断的bool对象 */}
  if (isLoggedIn) {  {/* 当isLoggedIn为ture时执行 */}
    return <h1>渲染Ture</h1>
  } else {  {/* 否则执行 */}
    return <h2>渲染False</h2>
  }
}
```
当判断`isLoggedIn`为`ture`时，则渲染该组件：
```jsx
return (
  <Greeting isLoggedIn={true}>
);
```

<a name="三元判断渲染"></a>
##### 2.5.2 三元判断渲染（使用格式：`{ bool-OBJ ? (bool=ture显示) : (bool=false渲染) }`）：

```jsx
function Notification({ message }) {
  return (
    <div>
      { message ? (  {/* message为被判断的bool对象 */}
        <div className="alert">{message}</div>  {/* message === ture时渲染 */}
      ) : (
        <div className="empty">No notification</div>  {/* message === false时渲染 */}
      )}
    </div>
  );
}
```
<a name="短路与判断渲染"></a>
##### 2.5.3 短路与判断渲染（使用格式：`{ bool-OBJ Y/N && (bool=ture时渲染)}`）：

```jsx
function Cart({ itemCount }){
  return(
    <div>
      { itemCount > 0 (
        <p>当前值为: {itemCount}</p>
      )}
    </div>
  );
}
```

<a name={列表渲染}></a>
#### 2.6 列表渲染

使用`map()`函数去实现对对象的列表渲染：
```jsx
// 创建一个list对象
const todos = ['Learn React', 'Build Project', 'Deploy App'];

function TodoList() {
  return (
    <ul>
      {todos.map((todo, index => (
      // 对list对象'todos'使用map方法遍历，todo为当前元素值、index为当前遍历索引位（map方法自动给出）
        <li key={index}>{todo}</li>
        // key是React识别列表渲染中列表项的唯一标识，一般直接是`key={index}`
      )))}
    </ul>
  );
}
```

<a name="钩子函数"></a>
#### 2.7 钩子函数

<a name="useState状态管理"></a>
##### 2.7.1 useState状态管理

用于定于、管理对象和对象的状态，如我需要定义一个bool对象为`'count'`，那么就需要使用State去定义、赋予初始值，以及管理`'count'`对象，如下：
```jsx
import { useState } from 'react';  // 导入useState状态管理

function Counter() {
  const [count, setCount] = useState(0);
  // 创建count对象与setCount方法，并定义count的初始值为0；
  // count对象用于存储值，而setCount方法用于修改count对象（固定格式：set+对象名）
  return (
    {/* 使用onClick事件去调用setCount方法修改count对象的值 */}
    <button onClick={() => setCount(count + 1)}>
      Clicked {count} times
    </button>
  );
}
```

<a name="副作用管理"></a>
##### 2.7.2 useEffect副作用

在jsx渲染或某个对象出现变化时，副作用组件就会执行以处理数据或执行指定逻辑，有三种触发逻辑：

<a name="全量监控模式"></a>
###### 全量监控模式：监控所有变化

```jsx
import { useEffect } from 'react';  // 导入useEffect副作用管理

function UserList() {
  useEffect(() => {
    console.log('hi');
  });  // 任何状态都会触发该副作用组件

  return(
    <div>
      ...
    </div>
  );
}
```

<a name="单次执行模式"></a>
###### 单次执行模式：仅执行一次

```jsx
import { useEffect, useState } from 'react';

function UserList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('目标url/users')
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []);  // 由空数组标识，当组件进入生命周期时即刻执行一次，且不重复

  return (
    <ul>
      {user.map(user => (
        <li key={user.id}>(user.name)</li>
      ))}
    </ul>
  );
}
```

<a name="精准监控模式"></a>
###### 精准监控模式：监控变量对象的变化

```jsx
import { useState, useEffect } from 'react';

funtion DocumentEditor({ originalDocument }) {
  const [currentDocument, setCurrentDocument] = useState(originalDocument);
  const [showWarning, setShowWarning] = useState(false);

  useEffect(() => {
    const hasChanges = JSON.stringify(currentDocument) !== JSON.stringify(originalDocument);
    setShowWarning(hasChanges);
  }, [currentDocument, originalDocument]);  
  // 监控当currentDocument与originalDocument其一出现变化时，副作用执行(双保险)
  // 注意，如果const体中存在两个变量对象时，就需要双监控，否则只需要监控useState定义的currentDocument变量

    return (
    <div>
      {/* 文档编辑区域 */}
      <textarea
        value={currentDocument.content}
        onChange={(e) => 
          setCurrentDocument({
            ...currentDocument,
            content: e.target.value
          })
        }
      />

      {showWarning && <div className="warning">⚠️ 你有未保存的修改！</div>}
      <button onClick={() => setCurrentDocument(originalDocument)}>
        重置为最新原稿
      </button>
    </div>
  );
}
```

<a name="定时触发模式"></a>
###### 定时触发模式：进入组件周期后按间隔时间执行

```jsx
import { useState, useEffect } from 'react';

function timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(prev => prev + 1);
    })；
  }, 1000);  // 该组件被定义为每1000ms执行一次
}
```

<a name="组件进阶"></a>
### 三、组件进阶

<a name="组件组合"></a>
#### 3.1 组件组合

通过单独创建一个`.jsx`组件容器作为子组件，之后再在另外一个组件中导入（一般位于同目录下），以下是示例：
单独创建组件容器`Card.jsx`作为子组件：
```jsx
// Card.jsx
export default function Card({ children }) {  // 创建一个Card子组件，children用于接收调用体的内容
  return <div className={styles.card}>{children}</div>;
}
```
在其他组件（主组件）导入子组件：
```jsx
// App.jsx
import Card from './components/Card/Card.jsx';  // 导入子组件Card.jsx

function App() {
  return (
    {/* 调用子组件，将标签内的h2、p、p作为children带入子组件中 */}
    <Card>
      <h2>用户信息</h2>
      <p>姓名：张三</p>
      <p>年龄：28</p>
    </Card>
  );
}
```
以下是结构体：
```python
src/
├── components/
│   ├── Card/
│   │   ├── Card.jsx  # 子组件
└── App.jsx  # 主要调用组件
```

<a name="HOC高阶组件"></a>
#### 3.2 HOC高阶组件

类似于Python的装饰器，可以在不修改原组件代码的情况下增添新功能，以下为示例：
假设有原始业务组件`UserDashboard`，我需要增添`加载状态`与`权限验证`的两个新功能，那么我就可以创建一个HOC组件去增添这两项功能：
```
src/
├── components/
│   ├── Button.jsx            # 原始业务组件
│   └── hoc/                  # 高阶组件目录，如果不复杂可以放在同目录下（看开发者习惯）
│       └── withLogger.jsx    # 创建日志功能 HOC
├── App.jsx
└── main.jsx
```
原始组件`Button.jsx`如下：
```jsx
function Button({ onClick, children }) {
  return (
    <button onClick={onClick}>
      {children}
    </button>
  );
}

export default Button;
```
创建`withLogger.jsx`作为HOC高阶组件补充`日志记录`新功能：
```jsx
const withLogger = (WrappedComponent) => {  // HOC组件的命名规则为'with+新功能'，WrappedComponent用于接收原始组件
  return function Enhanced(props) {  // 这里实际上才是增强组件的本身，需要被return固定命名'Enhanced'
    const handleClick = () => {  // 这里是新的功能
      console.log('按钮被点击', new Date().toLocateTimeString());
      props.onClick?.();
    };
    return <WrappedComponent {...props} onClick={handleClick} />;  // 暂时还不清楚，但这是用于返回新组件的
  };
};

export default withLogger;
```
组合原始组件`Button.jsx`与HOC`withLogger.jsx`使用：
```jsx
import Button from './Button.jsx';  //
import withLogger from './component/hoc/withLogger.jsx';

const ButtonWithLogger = withlogger(Button);  // 使用HOC组件包裹原始组件，实现功能组合功能

function App() {
  return (
    <div>
      <Button onClick={() => console.log('点击按钮')}>点击</Button>
      {/* 基础的注册按钮，可以实现点击功能 */}
      <ButtonWithLogger onClick={() => console.log('点击按钮，记录日志')}>点击</ButtonWithLogger>
      {/* 被HOC增强过的Button，可以在点击功能实现的同时，还实现日志记录的功能 */}
    </div>
  );
}

export default App;
```

<a name="路由配置"></a>
### 四、路由配置

下载路由管理器：
```cmd
npm install react-router-dom
```
在`main.jsx`配置路由管理组件：
```jsx
import { BrowserRouter } from 'react-router-dom';  // 导入路由管理器

ReactDOM.createRoot(document.getElementByid('root')).render(
  <BrowserRouter>  {/* 将路由管理应用在App.jsx中 */}
    <App />
  </BrowserRouter>
);
```
在`App.jsx`配置路由：
```jsx
import { Routes, Route, Link } from 'react-router-dom';  // 导入路由配置器

function App() {
  return (
    <>
      {/* 标记、定义路由 */}
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>
      {/* 将路由指向组件 */}
      <Routes>
        <Route path="/" element={<HomePage />} />
        <Route path="/about" element={<AboutPage />} />
      </Routes>
    </>
  );
}
```








<a name="项目运行"></a>
#### 项目运行

<a name="本地运行React"></a>
##### 3.1 本地运行React

通过在命令行`cd /项目目录`进入项目根目录，启动项目的本地运行（测试用）：
```cmd
npm run dev
```



---
动态加载CSS样式：
```jsx
function Notification({ message, type }){
  return(
    <div className={type === 'error' ? styles.error : styles.info}>
      {message || 'No message'}
    </div>
  );
}
```
