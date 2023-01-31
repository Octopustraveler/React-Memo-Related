# refs 属性

> 组件内标签可以定义 ref 属性来标识自己

## createRef 写法

```js
class Demo extends React.Component {
  //React.creatRef 调用后返回一个容器，可以存储被 ref 标识的节点，但只能保存一个
  myRef = React.creatRef();
  showData = () => {
    console.log(this.myRef); // {current: input}
  };

  render() {
    return <input ref={this.myRef} />;
  }
}
```

## 回调函数写法

### 内联函数

```js
class Demo extends React.Component {
  showData = () => {...};
  render() {
    return (
      // 将当前 ref 所处的节点挂在实例自身上，名为 input1，从 this 自身取 ref
      // 简写：ref = {c => this.input1 = c}
      <div>
        <input
          ref={(currentNode) => {
            this.input1 = currentNode;
          }}
          placeholder="click button to alert"
        />
        <button onBlur={this.showData}>click me</button>
      </div>
    );
  }
}
```

### class 绑定函数

```js
class Demo extends React.Component {
  showData = () => {...};
  saveInput = (currentNode) => {
    this.input1 = currentNode;
  }
  render() {
    return (
      <div>
        <input ref={this.saveInput} placeholder="click button to alert" />
        <button onBlur={this.showData}>click me to alert input data</button>
      </div>
    );
  }
}
```

#### ref 内回调函数执行几次？

- 如果 `ref` 回调函数是以内联函数定义的，在更新过程中它会被执行两次，第一次传入参数 `null`，第二次会传入参数 DOM 元素。

- 因为每次渲染时会创建一个新的函数实例，所以 `React` 清空旧的并设置新的。

- 解决办法：使用类绑定函数写法。

## String 写法（不推荐，存在运行效率问题，可能在未来版本移除）

```js
class Demo extends React.Component {
  showData = () => {
    console.log(this.refs); // refs 包含所有 ref 标签的内容
    const { input1 } = this.refs; // 解构
    alert(input1.value);
  };

  render() {
    return (
      <div>
        <input ref="input1" placeholder="click button to alert" />
        <button onClick={this.showData}>click me to alert input data</button>
      </div>
    );
  }
}
ReactDOM.render(...);
```

## 事件处理

1. 通过 onXXX 属性指定事件处理函数（注意大小写）;

2. React 使用的是自定义（合成）事件，而不是使用的原生 DOM 事件 ———— 为了更好的兼容性;

3. React 中的事件是通过事件委托方式处理的（委托给最外层元素） ———— 为了高效;

4. 不要过度使用 `refs`（通过 event.target 得到发生事件的 DOM 元素对象）;
