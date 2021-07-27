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

