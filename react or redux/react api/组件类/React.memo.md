##### 3- memo

React.memo和PureComponent 的区别和共同点

共同点： 都可以用作性能优化

不同点：1- React.memo 使用范围更广，高阶组件、函数组件、类组件都能使用， PureComponent 只能类组件继承

​				2- React.memo只对props进行浅比较决定是否渲染， PureComponent针对props 和State

React.memo接受两个参数，第一个参数原始组件本身，第二个参数，可以根据一次更新中`props`是否相同决定原始组件是否重新渲染。是一个返回布尔值，`true` 证明组件无须重新渲染，`false`证明组件需要重新渲染，这个和类组件中的`shouldComponentUpdate()`正好相反 。

**React.memo: 第二个参数 返回 `true` 组件不渲染 ， 返回 `false` 组件重新渲染。**

**shouldComponentUpdate: 返回 `true` 组件渲染 ， 返回 `false` 组件不渲染。**



控制组件在仅此一个`props`数字变量，一定范围渲染。

例子🌰：

控制 `props` 中的 `number` ：

- 1 只有 `number` 更改，组件渲染。
- 2 只有 `number` 小于 5 ，组件渲染。

```react 
function TextMemo(props){
  console.log('子组件渲染')
  if(props) {
    return <div>hello, world</div>
  }
}

const controlIsRender = (pre, next) => {
  if(pre.number === next.number){ // 相等不渲染
    return true
  } else if(pre.number !== next.number && next.number > 5){ // number改变，但值大于5，不渲染组件
    return true
  } else{
    return false
  }
}

const NewTextMemo = memo(TextMemo, controlIsRender)
class Index extends React.Component{
    constructor(props){
        super(props)
        this.state={
            number:1,
            num:1
        }
    }
    render(){
        const { num , number }  = this.state
        return <div>
            <div>
                改变num：当前值 { num }  
                <button onClick={ ()=>this.setState({ num:num + 1 }) } >num++</button>
                <button onClick={ ()=>this.setState({ num:num - 1 }) } >num--</button>  
            </div>
            <div>
                改变number： 当前值 { number } 
                <button onClick={ ()=>this.setState({ number:number + 1 }) } > number ++</button>
                <button onClick={ ()=>this.setState({ number:number - 1 }) } > number -- </button>  
            </div>
            <NewTexMemo num={ num } number={number}  />
        </div>
    }
}
```

