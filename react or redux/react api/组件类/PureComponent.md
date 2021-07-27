##### 2- PureComponent

`PureComponent`和 `Component`用法，差不多一样，唯一不同的是，纯组件`PureComponent`会浅比较，`props`和`state`是否相同，来决定是否重新渲染组件。所以一般用于**性能调优**，减少**render**次数。

```react
class Index extends React.PureComponent{
    constructor(props){
        super(props)
        this.state={
           data:{
              name:'alien',
              age:28
           }
        }
    }
    handerClick= () =>{
        const { data } = this.state
        data.age++
        this.setState({ data })
    }
    render(){
        const { data } = this.state
        return <div className="box" >
        <div className="show" >
            <div> 你的姓名是: { data.name } </div>
            <div> 年龄： { data.age  }</div>
            <button onClick={ this.handerClick } >age++</button>
        </div>
    </div>
    }
}
```

**点击按钮，没有任何反应**，因为`PureComponent`会比较两次`data`对象，都指向同一个`data`,没有发生改变，所以不更新视图。

解决这个问题很简单，只需要在`handerClick`事件中这么写：

```react
 this.setState({ data:{...data} })
```

**浅拷贝**就能根本解决问题。