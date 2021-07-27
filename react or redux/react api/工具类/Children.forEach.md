`Children.forEach`和`Children.map` 用法类似，`Children.map`可以返回新的数组，`Children.forEach`仅停留在遍历阶段。

我们将上面的`WarpComponent`方法，用`Children.forEach`改一下。

```react
function WarpComponent(props){
    React.Children.forEach(props.children,(item)=>console.log(item))
    return props.children
}   
```