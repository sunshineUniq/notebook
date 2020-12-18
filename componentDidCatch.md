render  报错就会触发钩子componentDidCatch

 React 16 将提供一个内置函数 `componentDidCatch`，如果 `render()` 函数抛出错误，则会触发该函数。

```javascript
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  componentDidCatch(error, info) {
    // Display fallback UI
    this.setState({ hasError: true });
    // You can also log the error to an error reporting service
    logErrorToMyService(error, info);
  }

  render() {
    if (this.state.hasError) {
      // You can render any custom fallback UI
      return <h1>Something went wrong.</h1>;
    }
    return this.props.children;
  }
}
```

当然你可以把这个组件封装下成为

```javascript
<ErrorBoundary>
  <MyWidget />
</ErrorBoundary>
```

##  另一个特性：

`componentDidCatch` 是包含错误堆栈的 info 对象

```
{this.state.info && this.state.info.componentStack}
```

当然我是这么用的在路由那边

```javascript
class App extends React.Component {
  constructor(props) {
    super(props)
    this.state = {
      hasError: false
    }
  }
  componentDidCatch(error, info) {
    console.log(error, info)
    this.setState({
      hasError: true
    })
  }
  render() {
    return this.state.hasError ?
      <h2>页面出错了404</h2>
      : (
        <React.Fragment>
          {/* 检验是否有登录信息 */}
          <AutoRoute />
          {/* 有了switch后，匹配到path后就不会再匹配下去了 */}
          <Switch>
            <Route path="/login" component={Login}></Route>
            <Route path='/register' component={Register}></Route>
            <Route path='/chat/:user' component={Chat}></Route>
          </Switch>
        </React.Fragment>
      )
  }
}
```

注意： 在开发环境看不到效果