`createContext`用于创建一个`Context`对象，`createContext`对象中，包括用于传递 `Context` 对象值 `value`的`Provider`，和接受`value`变化订阅的`Consumer`。

```react
const MyContext = React.createContext(defaultValue)
```

`createContext`接受一个参数`defaultValue`，如果`Consumer`上一级一直没有`Provider`,则会应用`defaultValue`作为`value`。**只有**当组件所处的树中没有匹配到 `Provider` 时，其 `defaultValue` 参数才会生效。

```react

function ComponentB(){
    /* 用 Consumer 订阅， 来自 Provider 中 value 的改变  */
    return <MyContext.Consumer>
        { (value) => <ComponentA  {...value} /> }
    </MyContext.Consumer>
}

function ComponentA(props){
    const { name , mes } = props
    return <div> 
            <div> 姓名： { name }  </div>
            <div> 想对大家说： { mes }  </div>
         </div>
}

function index(){
    const [ value , ] = React.useState({
        name:'alien',
        mes:'let us learn React '
    })
    return <div style={{ marginTop:'50px' }} >
        <MyContext.Provider value={value}  >
          <ComponentB />
    </MyContext.Provider>
    </div>
}

// 姓名： alien
// 想对大家说：let us learn React
```

`Provider`和`Consumer`的良好的特性，可以做数据的**存**和**取**，`Consumer`一方面传递`value`,另一方面可以订阅`value`的改变。

`Provider`还有一个特性可以层层传递`value`，这种特性在`react-redux`中表现的淋漓尽致。