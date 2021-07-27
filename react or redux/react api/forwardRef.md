1- 隔代获取子孙组件

```react
function Son(props){
  const {grandRef} = props
  return <div>
  	<div>i am allen</div>
    <span ref={grandRef}>这就是想要获取的元素</span>
  </div>
}

class Father extends React.Component{
  constructor(props) {
    super(props)
  }
  render() {
    return <div>
    	<Son grandRef={this.props.grandRef}/>
    </div>
  }
}

const NewFather = React.forwardRef((props, ref) => <Father grandRef={ref} {...props}/>)
                                   
class GrandFather extends React.Component {
  constructor(props){
  	super(props)
  }
	node = null
  componentDidMount() {
    console.log(this.node)
  }
	render() {
    return <div>
    	<NewFather ref={(node) => this.node = node}/>
    </div>
  }
}

```

高阶组件转发ref 

```react
function HOC(Component) {
  class Wrap extends React.Component{
    render(){
      const {forwardedRef, ...otherprops} = props
      return <Component ref={forwardedRef} {...otherprops}/>
    }
  }
  return React.forwardRef((props, ref) => <Wrap forwardRef={ref} {...props}/>)
}
class Index extends React.Component{
  componentDidMount(){
      console.log(666)
  }
  render(){
    return <div>hello,world</div>
  }
}
const HocIndex =  HOC(Index,true)
export default ()=>{
  const node = useRef(null)
  useEffect(()=>{
     /* 就可以跨层级，捕获到 Index 组件的实例了 */ 
    console.log(node.current.componentDidMount)
  },[])
  return <div><HocIndex ref={node}  /></div>
}
```

