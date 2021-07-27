验证 `children` 是否只有一个子节点（一个 `React` 元素），如果有则返回它，否则此方法会抛出错误。

```react
function WarpComponent(props){
    console.log(React.Children.only(props.children))
    return props.children
}   
function Index(){
    return <div style={{ marginTop:'50px' }} >
        <WarpComponent>
            { new Array(3).fill(0).map((item,index)=><Text key={index} />) }
            <span>hello,world</span>
        </WarpComponent>
    </div>
}
```

```react
function WarpComponent(props){
    console.log(React.Children.only(props.children))
    return props.children
}   
function Index(){
    return <div style={{ marginTop:'50px' }} >
        <WarpComponent>
           <Text/>
        </WarpComponent>
    </div>
}
```

`React.Children.only()` 不接受 `React.Children.map()` 的返回值，因为它是一个数组而并不是 `React` 元素。

