`Portal` 提供了一种将子节点渲染到存在于父组件以外的 `DOM` 节点的优秀的方案。`createPortal` 可以把当前组件或 `element` 元素的子节点，渲染到组件之外的其他地方。

应用场景：

全局的弹窗组件```model```

`<Model/>`组件一般都写在我们的组件内部，倒是真正挂载的`dom`，都是在外层容器，比如`body`上。此时就很适合`createPortal`API。

`createPortal`接受两个参数：

```react
ReactDOM.createPortal(child, container)
```

参数child： 任何可渲染的React子元素

参数container: DOM元素

```react
function WrapComponent({children}){
  const domRef = useRef(null)
  const [PortalComponent, setPortalComponent] = useState(null)
  React.useEffect(() => {
    setPortalComponent(ReactDOM.createPortal(children, domRef.current))
  }, [])
  return <div>
  	<div className="container" ref={domRef}></div>
    {PortalComponent}
  </div>
}

class Index extends React.Component{
  render(){
    return <div style={{marginTop: '50px'}}>
    	<WrapComponent>
      	<div>hello, world</div>
      </WrapComponent>
    </div>
	}
}
```

![image-20210728173922935](/Users/sunshine/Desktop/zm/img/createPortal.png)

我们可以看到，我们`children`实际在`container` 之外挂载的，但是已经被`createPortal`渲染到`container`中。



