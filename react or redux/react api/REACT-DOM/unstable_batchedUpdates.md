在`react-legacy`模式下，对于事件，`react`事件有批量更新来处理功能, 但是这一些非常规的事件中，批量更新功能会被打破。所以我们可以用`react-dom`中提供的`unstable_batchedUpdates` 来进行批量更新。

**一次点击实现的批量更新**：渲染一次

```react
class Index extends React.Component{
  constructor(props){
    super(props)
    this.state={
      number:1
    }
  }
  handleClick = () => {
    this.setState({number: this.state.number +1})
    console.log(this.state.number)
    this.setState({number: this.state.number +1})
    console.log(this.state.number)
    this.setState({number: this.state.number +1})
    console.log(this.state.number)
  }
  render() {
    return <div style={{ marginTop:'50px' }}>
    	<button onClick={this.handleClick}>click me</button>
    </div>
  }
}

// 1
// 1
// 1
```

**批量更新条件被打破**： 渲染三次

```react
class Index extends React.Component{
  constructor(props){
    super(props)
    this.state={
      number:1
    }
  }
  handleClick = () => {
    Promise.resolve().then(()=>{
      this.setState({number: this.state.number +1})
    console.log(this.state.number)
    this.setState({number: this.state.number +1})
    console.log(this.state.number)
    this.setState({number: this.state.number +1})
    console.log(this.state.number)
    })
  }
  render() {
    return <div style={{ marginTop:'50px' }}>
    	<button onClick={this.handleClick}>click me</button>
    </div>
  }
}

// 1
// 2
// 3
```

**unstable_batchedUpdate助力**： 渲染一次

```react
class Index extends React.Component{
  constructor(props){
    super(props)
    this.state={
      number:1
    }
  }
  handleClick = () => {
    Promise.resolve().then(()=>{
      ReactDOM.unstable_batchedUpdate(()=> {
        this.setState({number: this.state.number +1})
    		console.log(this.state.number)
   		 	this.setState({number: this.state.number +1})
    		console.log(this.state.number)
    		this.setState({number: this.state.number +1})
    		console.log(this.state.number)
      })
    })
  }
  render() {
    return <div style={{ marginTop:'50px' }}>
    	<button onClick={this.handleClick}>click me</button>
    </div>
  }
}
// 1
// 2
// 3
```

