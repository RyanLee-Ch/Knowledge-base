<h1 style="text-align: center;">React</h1>

- [一、项目创建](#项目创建)
- [二、组件](#组件)
    - [1 组件的定义](#组件的定义)
    - [2 创建组件](#创建组件)
        - [2.1 组件目录创建](#组件目录创建)
        - [2.2 创建组件.jsx](#创建组件.jsx)

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

##### 2.3 创建组件样式.module.scss
举例创建`Button.jsx`的组件样式`Button.module.scss`：
```css
.button {
  padding: 12px 24px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  transition: background-color 0.3s;

  // SCSS 嵌套语法
  &:hover {
    background-color: darken(#4CAF50, 10%);
  }

  // 支持动态类名
  &--secondary {
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
> 补充：选择器分有很多类，有：标签选择器、类选择器、ID选择器、通配符选择器 等；

1. 标签选择器：`div { color: red; }`：将所有div标签的color设置为red；
2. 类选择器：`.button { padding: 10px; }`：设定一个名为button的类选择器，能够被`className={styles.button}`标记的**多个标签**调用
3. ID选择器：`#header { height: 60px; }`：设定一个名为header的ID选择器，能够被`id={header}`标记的
