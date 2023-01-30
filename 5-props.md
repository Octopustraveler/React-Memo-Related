# props

## 基本使用

```js
// 容器
<body>
  <div id="test1"></div>
</body>;

class Person extends React.Component {
  render() {
    const { name, sex, age } = this.props;
    return (
      <ul>
        <li>name: {name}</li>
        <li>sex: {sex}</li>
        <li>age: {age}</li>
      </ul>
    );
  }
}

// 传入的属性可以在原型 props 的身上看到
ReactDOM.render(
  <Person name="Tom" age="18" sex="male" />,
  document.getElementById("test1")
);
```

## 批量传递 props

使用 ES6 语法进行批量传递

```js
const p1 = {name = 'Alice' age="18" sex="female"}
ReactDOM.render(<Person {...p1} />,document.getElementById('test1'))

// 传递同时修改数据，修改 name
ReactDOM.render(<Person {...p1, name:'jack'} />,document.getElementById('test1'))

// 传递同时合并数据，新增 address
ReactDOM.render(<Person {...p1, name:'jack', address:'earth'} />,document.getElementById('test1'))

```

- 展开运算符不能直接展开对象，需要用花括号包括，克隆一个新对象：let p2 = {...p1}

- 不同于 `ReactDOM` 中的展开运算符，花括号代表 `js` 表达式，`React` 通过 `Babel` 实现展开对象，并且只适用于`标签`属性内的展开。

## 对 props 进行类型限制

> `React 16` 版本写法：

```js
// 引入 prop-types.js
<script type="text/javascript" src="../js/prop-types.js"></script>
class Person extends React.Component {...}

// 类型限制
Person.propTypes = {
  name: PropTypes.string.isRequired, // 字符类型，且必需项
  age: PropTypes.number,
  speak: propTypes.func // 函数类型，为避免命名冲突，使用 func
}

// 默认值
Person.defaultProps = {
  sex: 'neutral',
  age: 18
}

```

> `React 15` 旧版本写法：依赖 React

```js
class Person extends React.Component {...}
Person.propTypes = {
  // 注意大小写，指明 name 为 string 类型
  name: React.PropTypes.string
}

```

## 简写 props, 把属性合并在类当中

```js
class Person extends React.Component {
  static propTypes = {...},
  static defaultProps = {...}
}


```

> static 是类变量(方法)，只有一份副本，被该类所有实例共享。

## 函数式组件使用 props

> 函数可以传参，利用 props 接收参数

```js
function Person(props) {
  const { name, age, sex } = props;
  return (
    <ul>
      <li>name: {name}</li>
      <li>sex: {age}</li>
      <li>age: {sex}</li>
    </ul>
  );
}

// 类型限制与默认值
Person.propTypes = {...}
Person.defaultProps = {...}

ReactDOM.render(
  <Person name="Tom" age="18" sex="male" />,
  document.getElementById("test1")
);
```

> 函数式组件不能直接使用其他功能如：state, refs
