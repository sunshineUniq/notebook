```react
React.createFactory(type)
```

返回用于生成指定类型 React 元素的函数。类型参数既可以是标签名字符串（像是 '`div`' 或 '`span`'），也可以是 React 组件 类型 （ `class` 组件或函数组件），或是 `React fragment` 类型。

```react
const Text = React.createFactory(()=><div>hello,world</div>) 
function Index(){  
    return <div style={{ marginTop:'50px'  }} >
        <Text/>
    </div>
}
```

这个`api`将要被废弃，我们这里就不多讲了，如果想要达到同样的效果，请用`React.createElement`

