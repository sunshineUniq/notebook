## unmountComponentAtNode

从 `DOM` 中卸载组件，会将其事件处理器和 `state` 一并清除。如果指定容器上没有对应已挂载的组件，这个函数什么也不会做。如果组件被移除将会返回 `true` ，如果没有组件可被移除将会返回  `false` 。

```react
function Text(){
  return <div>hello, world</div>
}
class Index extends React.Component{
  node = null
	constructor(props) {
    super(props)
  }
	componentDidMount(){
      /*  组件初始化的时候，创建一个 container 容器 */
        ReactDOM.render(<Text/> , this.node )
  }
	handerClick = () => {
     /* 点击卸载容器 */ 
		const state = ReactDOM.unmountComponentAtNode(this.node)
    console.log(state)
  }
	render(){
    return <div style={{marginTop: '50px'}}>
    	<div ref={(node)=> this.node = node}></div>
      <button onClick={this.handerClick}>click me</button>
    </div>
  }
}
```

