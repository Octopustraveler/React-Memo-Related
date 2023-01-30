# React 事件绑定

## 标准写法

- 首先初始化状态`state`，将数据写在里边。

- `React`已重写了一些原生操作如：`onclick`，在绑定事件中要使用驼峰写法。

- 绑定函数时，使用花括号包括函数名，不能使用引号或`onClick={demo()}`，不然会将函数返回值赋值给 `onClick` 失去作用。

```js
// 1. 创建组件
class Weather extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isHot: false };
    // 解决方法中this指向问题，右边在原型链上生成changeWeather，将其this指向实例中的changeWeather
    this.changeWeather = this.changeWeather.bind(this);
  }
  render() {
    const { isHot } = this.state;
    return <h1 onClick={changeWeather}>今天天气很{isHot ? "hot" : "cold"}</h1>;
  }

  function changeWeather() {
    // 1. 类中方法默认开启了局部严格模式，所以 this 为 undefined
    // 2. 不能直接修改 state 中的数据，通过原型身上的 setState 更新 —— 合并，而不是替换
    this.setState({isHot:!isHot})
  }
}

// 2. 渲染组件到页面
ReactDOM.render(<Weather />, getElementById("test"));
```

- 构造器调用几次？———— 因为在 `render` 中只调用了一次，所以是一次;

- `render` 调用几次？———— 1+n 次，1 是初始化，n 是状态更新的次数;

## 简写形式

```js
class Weather extends React.Component {
    state = {...}
    render(){...}
    changeWeather = () => {...}
}
```

- 因为类中可直接写赋值语句，将 `state` 写在构造器外边;

- 自定义方法使用赋值语句 + 箭头函数;

- 箭头函数没有自己的 `this` 会向外层寻找，解决丢失 `this` 问题;

- 原型身上不再有该方法，不需要构造器函数;
