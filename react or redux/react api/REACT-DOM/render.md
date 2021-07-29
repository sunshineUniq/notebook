用于渲染一个`react`元素，一般`react`项目我们都用它，渲染根部容器`app`。

```react
ReactDOM.render(element, container[, callback])
```

```react
ReactDOM.render(
	<App/>,
  document.getElementById('app')
)
```

`ReactDOM.render`会控制`container`容器节点里的内容，但是不会修改容器节点本身。

