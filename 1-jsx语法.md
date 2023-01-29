# 创建虚拟 DOM 的两种方法

- 引入 react 核心库: `react.development.js`

- 引入 react-dom，用于支持 react 操作 DOM: `react-dom.development.js`

- 引入 babel，用于将 jsx 转为 js: `babel.min.js`

- 指定 script 类型: `<script type="text/babel">`

```js
// 1. 创建虚拟DOM

// jsx语法创建，非字符串，不加引号，类型要指定text/babel
const VDOM = <h1 id="test"> Hello React </h1>;

// 函数创建虚拟DOM (繁琐，一般不使用)
const VDOM = React.createElement("h1", { id: test }, "Hello React");

// 2. 渲染虚拟DOM到页面
ReactDOM.render(VDOM, document.getElementById("test"));
```

## jsx 语法规则

### 1. 定义虚拟 DOM 时，不能写引号

```js
const VDOM = <h1>Hello React</h1>;
```

### 2. 标签混入 JS 表达式时要用花括号: {}

```js
const frameName = "React"
<h1>Hello {frameName}</h1>
```

### 3. 样式的类名指定不能用 class，要用 calssName

```js
<style>
  .title{
     background-color: skyblue;
     width: 200px;
  }
</style>

// script
<h1 className="title">Hello React</h1>
```

> 为了防止与 ES6 新引入的 class 类名冲突，使用 className。直接用 class 有效果但会显示警告，低版本会报错。

### 4. 内联样式要用 style={{key:value}}形式

```js
<h1 style={{ color: "orange", fontSize: "22px" }}>Hello React</h1>
```

> 第一层花括号代表 JS 表达式，第二层代表键值对。如果样式名由多个单词组成，使用驼峰形式。

### 5. 虚拟 DOM 只有一个根标签（Vue2 模板中也只能有一个根标签）

```js
<h1 style={{ color: "orange", fontSize: "22px" }}>Hello React</h1>
```

### 6. 标签首字母

1. 若`小写字母`开头，则将该标签转为`html`中同名元素，若无该标签对应元素则报错;

2. 若`大写字母`开头，`react`就去渲染对应的组件，若组件没有定义，则报错;

## 练习

- 注意区分：JS 语句(代码) 与 JS 表达式

  1. 表达式：一个表达式会产生一个值，可以放在任何一个需要值得地方：

     - a
     - a+b
     - demo()
     - arr.map()
     - function test () {}

  2. 语句(代码)：
     - if(){}
     - for(){}
     - switch(){}
     - ...

- 给一个数组，将数组内数据以列表样式展示在网页：

```js
const data = ["Angular", "React", "Vue"];
const VDOM = (
  <div>
    <h1>Front Web UI</h1>
    <ul>
      // 需要给节点指定唯一的key
      {data.map((item, index) => {
        return <li key={index}>{item}</li>;
      })}
    </ul>
  </div>
);
```

> Objects are not valid as a React child: 不能使用对象作为 React 子节点
