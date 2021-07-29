## findDOMNode

作用： 用于访问组件DOM元素节点

```react```推荐使用```ref```模式， 不期望使用```findDOMNode```

```react
ReactDOM.findDOMNode(component)
```

注意点：

- 1 `findDOMNode`只能用在已经挂载的组件上。
- 2  如果组件渲染内容为 `null` 或者是 `false`，那么 `findDOMNode`返回值也是 `null`。
- 3 `findDOMNode` 不能用于函数组件。

```react
class Index extends React.Component{
  handerFindDom = () => {
    console.log(ReactDOM.findDOMNode(this))
  }
  render() {
    return <div style={{ marginTop:'100px' }} >
            <div>hello,world</div>
            <button onClick={ this.handerFindDom } >获取容器dom</button>
        </div>
  }
}

// <div style={{ marginTop:'100px' }} >
//            <div>hello,world</div>
//           <button onClick={ this.handerFindDom } >获取容器dom</button>
//        </div>
```

我们完全可以将外层容器用`ref`来标记，获取捕获原生的`dom`节点。