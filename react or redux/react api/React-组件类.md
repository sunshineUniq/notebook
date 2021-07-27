### 组件类

组件类API

- Component

- PureComponent

- memo 高阶组件

- forwardRef 高阶组件

- lazy

- Suspense

- Fragment

- Profiler

- StrictMode

  

##### 1- Component

`react`对`Component`做了些什么。

```react/src/ReactBaseClasses.js```

```react
function Component(props, context, updater) {
  this.props = props;
  this.context = context;
  this.refs = emptyObject;
  this.updater = updater || ReactNoopUpdateQueue;
}
```

这就是`Component`函数，其中`updater`对象上保存着更新组件的方法。

**我们声明的类组件是什么时候以何种形式被实例化的呢？**

```react-reconciler/src/ReactFiberClassComponent.js```

contrustClassInstance

```react
function constructClassInstance(
	workInProgress,
  ctor,
  props
) {
	const instance = new ctor(props, context)
  instance.updater = {
    isMounted,
    enqueueSetState() {
      /* setState触发这里面的逻辑 */
    }，
    enqueueReplaceState() {},
    enqueueForceUpdate(){
      /* forceUpdate 触发这里的逻辑 */
    }
  }
}
```

对于Component, react 处理逻辑还是很简单的， 实例化我们类组件，然后赋值updater 对象， 负责组件的更新。然后在组件的各个阶段，执行类函数的render函数和对应的生命周期函数

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

##### 3- memo

React.memo和PureComponent 的区别和共同点

共同点： 都可以用作性能优化

不同点：1- React.memo 使用范围更广，高阶组件、函数组件、类组件都能使用， PureComponent 只能类组件继承

​				2- React.memo只对props进行浅比较决定是否渲染， PureComponent针对props 和State

React.memo接受两个参数，第一个参数原始组件本身，第二个参数，可以根据一次更新中`props`是否相同决定原始组件是否重新渲染。是一个返回布尔值，`true` 证明组件无须重新渲染，`false`证明组件需要重新渲染，这个和类组件中的`shouldComponentUpdate()`正好相反 。

**React.memo: 第二个参数 返回 `true` 组件不渲染 ， 返回 `false` 组件重新渲染。**

**shouldComponentUpdate: 返回 `true` 组件渲染 ， 返回 `false` 组件不渲染。**

##### 4- forwardRef

- 转发引入Ref

这个场景实际很简单，比如父组件想获取孙组件，某一个`dom`元素。这种隔代`ref`获取引用，就需要`forwardRef`来助力。

`react`不允许`ref`通过`props`传递，因为组件上已经有 `ref` 这个属性,在组件调和过程中，已经被特殊处理，`forwardRef`出现就是解决这个问题，把`ref`转发到自定义的`forwardRef`定义的属性上，让`ref`，可以通过`props`传递。

- 高阶组件转发Ref

由于属性代理的`hoc`，被包裹一层，所以如果是类组件，是通过`ref`拿不到原始组件的实例的，不过我们可以通过`forWardRef`转发`ref`

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

##### 6- Suspense

何为`Suspense`, `Suspense` 让组件“等待”某个异步操作，直到该异步操作结束即可渲染。

```react
const ProfilePage = React.lazy(() => import('./ProfilePage')); // 懒加载
<Suspense fallback={<Spinner />}>
  <ProfilePage />
</Suspense>
```

##### 7- Fragment

和`Fragment`区别是，`Fragment`可以支持`key`属性。`<></>`不支持`key`属性。

##### 8- Profiler

`Profiler`这个`api`一般用于开发阶段，性能检测，检测一次`react`组件渲染用时，性能开销。

`Profiler` 需要两个参数：

第一个参数：是 `id`，用于表识唯一性的`Profiler`。

第二个参数：`onRender`回调函数，用于渲染完成，接受渲染参数

```react
const index = () => {
  const callback = (...arg) => console.log(arg)
  return <div >
    <div >
      <Profiler id="root" onRender={ callback }  >
        <Router  >
          <Meuns/>
          <KeepaliveRouterSwitch withoutRoute >
              { renderRoutes(menusList) }
          </KeepaliveRouterSwitch>
        </Router>
      </Profiler> 
    </div>
  </div>
}
```

![image-20210727143213910](../../img/profiler.png)

0 -id: `root` ->  `Profiler` 树的 `id` 。

1 -phase: `mount` ->  `mount` 挂载 ， `update` 渲染了。

2 -actualDuration: `6.685000262223184` -> 更新 `committed` 花费的渲染时间。

3 -baseDuration:  `4.430000321008265` -> 渲染整颗子树需要的时间

4 -startTime : `689.7299999836832` ->  本次更新开始渲染的时间

5 -commitTime : `698.5799999674782` ->  本次更新committed 的时间

6 -interactions: `set{}` -> 本次更新的 `interactions` 的集合

##### 9- StrictMode

`StrictMode` 不会渲染任何可见的 `UI` 。它为其后代元素触发额外的检查和警告。

>严格模式检查仅在开发模式下运行；它们不会影响生产构建。

`StrictMode`目前有助于：

- ①识别不安全的生命周期。
- ②关于使用过时字符串 `ref API` 的警告
- ③关于使用废弃的 `findDOMNode` 方法的警告
- ④检测意外的副作用
- ⑤检测过时的 `context API`

