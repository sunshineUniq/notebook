##### 4- forwardRef

- 转发引入Ref

这个场景实际很简单，比如父组件想获取孙组件，某一个`dom`元素。这种隔代`ref`获取引用，就需要`forwardRef`来助力。

`react`不允许`ref`通过`props`传递，因为组件上已经有 `ref` 这个属性,在组件调和过程中，已经被特殊处理，`forwardRef`出现就是解决这个问题，把`ref`转发到自定义的`forwardRef`定义的属性上，让`ref`，可以通过`props`传递。

- 高阶组件转发Ref

由于属性代理的`hoc`，被包裹一层，所以如果是类组件，是通过`ref`拿不到原始组件的实例的，不过我们可以通过`forWardRef`转发`ref`



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

