

##### 5- lazy

> React.lazy 和 Suspense 技术还不支持服务端渲染。如果你想要在使用服务端渲染的应用中使用，我们推荐 Loadable Components 这个库

`React.lazy`和`Suspense`配合一起用，能够有动态加载组件效果。`React.lazy` 接受一个函数，这个函数需要动态调用 `import()`。它必须返回一个 `Promise` ，该 `Promise` 需要 `resolve` 一个 `default export` 的 `React` 组件。

我们模拟一个动态加载的场景。

```react
import Test from './comTest'
const LazyComponent =  React.lazy(()=> new Promise((resolve)=>{
      setTimeout(()=>{
          resolve({
              default: ()=> <Test />
          })
      },2000)
}))
class index extends React.Component{   
    render(){
        return <div className="context_box"  style={ { marginTop :'50px' } }   >
           <React.Suspense fallback={ <div className="icon" ><SyncOutlined  spin  /></div> } >
               <LazyComponent />
           </React.Suspense>
        </div>
    }
}
```

我们用`setTimeout`来模拟`import`异步引入效果。**Test**

```react
class Test extends React.Component{
    constructor(props){
        super(props)
    }
    componentDidMount(){
        console.log('--componentDidMount--')
    }
    render(){
        return <div>
            <img src={alien}  className="alien" />
        </div>
    }
}
```

##### 