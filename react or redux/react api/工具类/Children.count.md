`children` 中的组件总数量，等同于通过 `map` 或 `forEach` 调用回调函数的次数。对于更复杂的结果，`Children.count`可以返回同一级别子组件的数量。

```react
function WarpComponent(props){
    const childrenCount =  React.Children.count(props.children)
    console.log(childrenCount,'childrenCount')
    return props.children
}   
function Index(){
    return <div style={{ marginTop:'50px' }} >
        <WarpComponent>
            { new Array(3).fill(0).map((item,index) => new Array(2).fill(1).map((item,index1)=><Text key={index+index1} />)) }
            <span>hello,world</span>
        </WarpComponent>
    </div>
}

// 7 "childrenCount"
```



